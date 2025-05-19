---
id: xdnm5is9c8fznrn1m80gigz
title: Hist_Insert_stro
desc: ''
updated: 1747190672127
created: 1747190582742
---


## aggregate.kpay_daily_cust_activity
## History Insert

- stro - call test_cbs.sp_hist_kpay_daily_cust_activity('2023-12-01'::date,'2023-12-30'::date);

bash
```
Create or replace procedure test_cbs.sp_hist_kpay_daily_cust_activity(start_date date , end_date date)
LANGUAGE plpgsql
AS $$
DECLARE vstart_date DATE ;
DECLARE vend_date Date ;
BEGIN
    vstart_date := start_date;
    vend_date := end_date;

    RAISE INFO 'vstart_date: %',  vstart_date;
    RAISE INFO 'vend_date: %', vend_date;

    -- RETURN;

    delete from aggregate.kpay_daily_cust_activity where "date" :: date between vstart_date and vend_date;

    CREATE TEMP TABLE #Login_Activity (
    type character varying(5) ENCODE raw,
    date date ENCODE raw,
    cust_id character varying(150) ENCODE raw,
    times bigint ENCODE raw,
    amount numeric(38,2) ENCODE raw
    )
    DISTSTYLE EVEN ; 

    
insert into #Login_Activity
select
    'Login' as type,
    login_date as date,
    cust_id,
    count(cust_id) as times,
    0.00 as amount
-- into #Login_Activity
from
    base.kpay_cust_device kcd
where
    -- login_date >= '2024-01-01' and 
    login_date :: date between vstart_date and vend_date
group by
    date,
    cust_id ; 


    
/* RQEV2-IywNoaeDrL */
CREATE TEMP TABLE #txn_activity As
select
    'Trn' as type,
    trn_date as date,
    cust_id ,
    count(trn_id) as times,
    sum(amount) as amount
-- into #txn_activity
from
    (
    select
        trn_date,
        debit_cust_id as Cust_ID,
        trn_id,
        amount
    from
        base.kpay_action_in_trn
    where
        -- trn_date >= '2024-01-01' and 
        debit_party_type = 'Customer'
        and trn_status = 'Completed'
        and trn_date ::date between vstart_date and vend_date
union
    select
        trn_date ,
        credit_cust_id as Cust_Id,
        trn_id,
        amount
    from
        base.kpay_action_in_trn
    where
        -- trn_date >= '2024-01-01' and 
        credit_party_type = 'Customer'
        and trn_status = 'Completed'
        and trn_date ::date between vstart_date and vend_date
    )
group by
    trn_date,
    cust_id;

    
insert into aggregate.kpay_daily_cust_activity 
select
    cust_id,
    date,
    --max(case when type ='Login' then date end) as Login_date,
isnull(sum(case when type = 'Login' then times end),
    0) as login_times,
    --max(case when type ='Trn' then date end) as Trn_date,
isnull(sum(case when type = 'Trn' then times end),
    0) as Trn_times,
    isnull(sum(case when type = 'Trn' then amount end),
    0) as Trn_Amount
from
    (
    select
        *
    from
        #Login_Activity A
union all
    select
        *
    from
        #txn_activity B
)
group by
    cust_id,
    date ;

    drop table #Login_Activity ; 
    drop table #txn_activity ;

END;
$$ ;
```