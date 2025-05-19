---
id: fsdaag68gmtrqdswgh7lx0r
title: aggregate_kpay_cust_dau_count
desc: ''
updated: 1747204974735
created: 1747193144227
---

## Email
- Data Model || DAU, WAU , MAU Login and Tran (customer segmentation)


## onetime initial
bash
```
{{ config(
    materialized='table',
    tags = ['published']
) }}

-----------------------------Initial Data Model script for aggregate.kpay_cust_dau_count ()
------------------------cust_detail
WITH cust_detail AS 
(
SELECT
    *,
    CASE
        WHEN datediff(DAY,
        COALESCE(lag_date,
        CAST(reg_date AS date)),
        from_date) NOT IN (1, 0) THEN 1
        ELSE 0
    END AS scd_diff
FROM
    (
    SELECT
        DISTINCT 
    ROW_NUMBER() OVER(PARTITION BY cust_id
    ORDER BY
        from_date)AS srno,
        is_current,
        cust_id,
        cust_level,
        cust_trust_level_detail,
        CAST(reg_date AS date) reg_date,
        from_date,
        to_date,
        lag(to_date,
        1) OVER(PARTITION BY cust_id
    ORDER BY
        from_date,
        to_date) AS lag_date
    FROM
        {{ ref('kpay_cust_details') }}
        -------didn't use is_current=1 in order to get real cust_level at that time while running history data of data model
)cust_main
)

,
-----------------------------------login
-------------------------to check new login

min_login AS
(
SELECT
    cust_id,
    'KBZPay' AS channel,
    min(login_date) AS min_login_date
FROM
    {{ ref('stg_kpay_cust_device') }}
GROUP BY
    cust_id
UNION ALL
SELECT 
    customer_id,
    'KBZPay Market' AS channel,
    min(CAST(login_time AS date))AS min_login_date
FROM
    {{ ref('stg_kpay_market_customer_loginlog') }}
GROUP BY
    customer_id
)

,
------------------------

cust_login AS
(
SELECT 
    l.*,
    CASE
        WHEN l.login_date = l2.min_login_date THEN l.login_cust_id
        ELSE NULL
    END AS new_login_cust_id
FROM
    (
    SELECT
        DISTINCT 
    login_date,
        'KBZPay' AS channel,
        cust_id AS login_cust_id
    FROM
        {{ ref('stg_kpay_cust_device') }}
UNION ALL
    SELECT
        DISTINCT
    CAST(login_time AS date) AS login_date,
        'KBZPay Market' AS channel,
        customer_id AS login_cust_id
    FROM
        {{ ref('stg_kpay_market_customer_loginlog') }} m
    WHERE
        "role" NOT IN ('Teller', 'Seller') 
)l
INNER JOIN min_login l2
ON
    l.login_cust_id = l2.cust_id
    AND l.channel = l2.channel
)
,

cust_login_final AS
(
SELECT 
    cl.login_date,
    cl.channel,
    c.cust_level,
    c.cust_trust_level_detail,
    count(cl.login_cust_id) AS total_login_dau_count,
    count(cl.new_login_cust_id) AS new_login_dau_count
FROM
    cust_login cl
INNER JOIN cust_detail c
ON
    c.cust_id = cl.login_cust_id
    AND ((cl.login_date BETWEEN from_date AND to_date)
        OR (cl.login_date < c.from_date
            AND c.scd_diff = 1))
GROUP BY
    cl.login_date,
    cl.channel,
    c.cust_level,
    c.cust_trust_level_detail

)
-------------------------login end
,
-------------------------------trn
-------------------for Market Trn Active Users
market_trn AS
(
SELECT
        DISTINCT
        ord_date AS trn_date,
        'KBZPay Market' AS channel,
        biller_customer_id AS trn_cust_id,
        (CASE
        WHEN is_newcust_day = 'New' THEN biller_customer_id
        ELSE NULL
    END) AS new_trn_cust_id
FROM 
    {{ ref('market_order_sale_detail') }}
WHERE
    business_state IN ('Completed', 'ReadyToSend', 'AwaitingShipping', 'AwaitingReceive', 'AwaitingReview', 'AwaitingPayment')

)
,
---------------------end market trn--------------
-----------------to check miniapp new trn

mini_min_trn_date AS
(
SELECT 
    trn_cust_id,
    min(min_trn_date)AS min_trn_date
FROM
    (
    SELECT
        credit_cust_id AS trn_cust_id,
        min(trn_date) AS min_trn_date
    FROM
        {{ ref('kpay_daily_mini_app_trn_detail') }}
    WHERE
        credit_party_type IN ('Customer')
            AND trn_status = 'Completed'
        GROUP BY
            credit_cust_id
    UNION all
        SELECT
            debit_cust_id AS trn_cust_id,
            min(trn_date)AS min_trn_date
        FROM
            {{ ref('kpay_daily_mini_app_trn_detail') }}
        WHERE
            debit_party_type IN ('Customer')
                AND trn_status = 'Completed'
            GROUP BY
                debit_cust_id
)t
GROUP BY
    trn_cust_id
)
,
------------------for MiniApp Trn
mini_app AS
(
SELECT 
    m.*,
    CASE
        WHEN m.trn_date = m1.min_trn_date THEN m.trn_cust_id
        ELSE NULL
    END AS new_trn_cust_id
FROM
    (
    SELECT
        DISTINCT
        trn_date,
        'MINI APP' AS channel,
        credit_cust_id AS trn_cust_id
    FROM
        {{ ref('kpay_daily_mini_app_trn_detail') }}
    WHERE
        trn_status IN ('Completed')
            AND credit_party_type IN ('Customer')
                AND (trn_type NOT IN ('Reversal Transaction')
                    OR reason_type IN ('OnlinepaymentRefund for GuaranteePayment', 'OnlinepaymentRefund for TimelyArrive'))
                    AND trn_id NOT IN (
                    SELECT
                        link_transaction_id
                    FROM
                        {{ ref('kpay_reversal_trans') }})
            UNION all
                SELECT
                    DISTINCT
        trn_date,
                    'MINI APP' AS channel,
                    debit_cust_id AS trn_cust_id
                FROM
                    {{ ref('kpay_daily_mini_app_trn_detail') }}
                WHERE
                    trn_status IN ('Completed')
                        AND debit_party_type IN ('Customer')
                            AND (trn_type NOT IN ('Reversal Transaction')
                                OR reason_type IN ('OnlinepaymentRefund for GuaranteePayment', 'OnlinepaymentRefund for TimelyArrive'))
                                AND trn_id NOT IN (
                                SELECT
                                    link_transaction_id
                                FROM
                                    {{ ref('kpay_reversal_trans') }})
)m
INNER JOIN mini_min_trn_date m1
ON
    m.trn_cust_id = m1.trn_cust_id
)
,
---------------------end mini app
---------------------------for kpay Trn Active Users
------------------------------to check kpay new trn
kpay_min_trn_date AS
(
SELECT 
    trn_cust_id,
    min(min_trn_date)AS min_trn_date
FROM
    (
    SELECT
        credit_cust_id AS trn_cust_id,
        min(trn_date) AS min_trn_date
    FROM
        {{ ref('stg_kpay_action_in_trn') }}
    WHERE
        credit_party_type IN ('Customer')
            AND trn_status = 'Completed'
        GROUP BY
            credit_cust_id
    UNION
        SELECT
            debit_cust_id AS trn_cust_id,
            min(trn_date)AS min_trn_date
        FROM
            {{ ref('stg_kpay_action_in_trn') }}
        WHERE
            debit_party_type IN ('Customer')
                AND trn_status = 'Completed'
            GROUP BY
                debit_cust_id
)t
GROUP BY
    trn_cust_id
)
,
------------------- kpay all trn 
kpay_trn AS
(
SELECT  
    t.*,
    CASE
        WHEN t.trn_date = t2.min_trn_date THEN t.trn_cust_id
        ELSE NULL
    END AS new_trn_cust_id
FROM
    (
    SELECT
        DISTINCT
        trn_date,
        'KBZPay' AS channel,
        credit_cust_id AS trn_cust_id
    FROM
        {{ ref('stg_kpay_action_in_trn') }}
    WHERE
        trn_status IN ('Completed')
            AND credit_party_type IN ('Customer')
                AND trn_date :: date >= '2018-08-06'
                AND (trn_type NOT IN ('Reversal Transaction')
                    OR reason_type IN ('OnlinepaymentRefund for GuaranteePayment', 'OnlinepaymentRefund for TimelyArrive'))
                    AND trn_id NOT IN (
                    SELECT
                        link_transaction_id
                    FROM
                        {{ ref('kpay_reversal_trans') }})
            UNION
                SELECT
                    DISTINCT
        trn_date,
                    'KBZPay' AS channel,
                    debit_cust_id AS trn_cust_id
                FROM
                    {{ ref('stg_kpay_action_in_trn') }}
                WHERE
                    trn_status IN ('Completed')
                        AND debit_party_type IN ('Customer')
                            AND trn_date :: date >= '2018-08-06'
                            AND (trn_type NOT IN ('Reversal Transaction')
                                OR reason_type IN ('OnlinepaymentRefund for GuaranteePayment', 'OnlinepaymentRefund for TimelyArrive'))
                                AND trn_id NOT IN (
                                SELECT
                                    link_transaction_id
                                FROM
                                    {{ ref('kpay_reversal_trans') }})
)t
INNER JOIN kpay_min_trn_date t2
ON
    t.trn_cust_id = t2.trn_cust_id
)

,
------------------All Trn
all_trn AS
(
SELECT 
    tt.trn_date,
    tt.channel,
    c.cust_level,
    c.cust_trust_level_detail,
    count(trn_cust_id) AS total_trn_dau_count,
    count(new_trn_cust_id) AS new_trn_dau_count
FROM
    (
    SELECT
        *
    FROM
        kpay_trn
UNION ALL
    SELECT
        *
    FROM
        market_trn
UNION ALL
    SELECT
        *
    FROM
        mini_app
)tt
INNER JOIN cust_detail c
ON
    c.cust_id = tt.trn_cust_id
    AND ((tt.trn_date BETWEEN c.from_date AND c.to_date)
        OR (tt.trn_date < c.from_date
            AND c.scd_diff = 1))
GROUP BY
    tt.trn_date,
    tt.channel,
    c.cust_level,
    c.cust_trust_level_detail
)
-----------final output


SELECT 
    isnull(cc.login_date,
    a.trn_date) AS dau_date,
    isnull(cc.channel,
    a.channel) AS channel,
    isnull (cc.cust_level,
    a.cust_level) AS cust_level,
    isnull (cc.cust_trust_level_detail,
    a.cust_trust_level_detail) AS cust_trust_level_detail,
    (CASE
        WHEN EXTRACT(YEAR
    FROM
        a.trn_date) < 2022 THEN cc.total_login_dau_count
        ELSE isnull(cc.total_login_dau_count,
        0)
    END) AS total_login_dau_count,
    (CASE
        WHEN EXTRACT(YEAR
    FROM
        a.trn_date) < 2022 THEN cc.new_login_dau_count
        ELSE isnull(cc.new_login_dau_count,
        0)
    END) AS new_login_dau_count,  
    isnull(a.total_trn_dau_count,
    0) AS total_trn_dau_count,
    isnull(a.new_trn_dau_count,
    0)AS new_trn_dau_count
FROM
    cust_login_final cc
FULL OUTER JOIN all_trn a
ON
    cc.login_date = a.trn_date
    AND cc.channel = a.channel
    AND cc.cust_level = a.cust_level
    AND cc.cust_trust_level_detail = a.cust_trust_level_detail
```

## Increase
bash
```

```