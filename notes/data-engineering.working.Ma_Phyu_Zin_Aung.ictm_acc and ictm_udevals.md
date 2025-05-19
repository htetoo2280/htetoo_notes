---
id: o7uqos4gfxfpzzasupgi8yt
title: ictm_acc and ictm_udevals
desc: ''
updated: 1746174976529
created: 1744084036176
---

## icmt_acc
- glue - dev_ora-processed-sfcubs-ictm-acc_updated
- s3 - s3://dev/ho_ictm_acc/dev/ho_ictm_acc/
- source - SELECT * FROM SFCUBS.ICTM_ACC
- catalogdb - datalake-processed-kbzrptdcpdb
- catalogtable - dev_sfcubs_ictm_acc_update

### in redshift
- source - dl_processed_kbzrptdcpdb.dev_sfcubs_ictm_acc_update
- procedure - integration.to_test_cbs_dev_ictm_acc()
- dest - test_cbs.dev_ictm_acc

### serverless dev

- select count(*) from hol.dev_ictm_acc_06_mar_previous;
- select count(*) from hol.dev_ictm_acc


### Creating table

```bash
CREATE TABLE hol.dev_ictm_acc_06_mar_previous (
    brn character varying(9) ENCODE lzo,
    acc character varying(60) ENCODE lzo,
    calc_acc character varying(60) ENCODE lzo,
    book_acc character varying(60) ENCODE lzo,
    has_is character varying(3) ENCODE lzo,
    int_start_date timestamp without time zone ENCODE az64,
    last_is_date timestamp without time zone ENCODE az64,
    acc_type character varying(3) ENCODE lzo,
    book_brn character varying(9) ENCODE lzo,
    auto_rollover character varying(3) ENCODE lzo,
    close_on_maturity character varying(3) ENCODE lzo,
    move_int_to_unclaimed character varying(3) ENCODE lzo,
    move_pric_to_unclaimed character varying(3) ENCODE lzo,
    maturity_date timestamp without time zone ENCODE az64,
    princ_liq_ac character varying(60) ENCODE lzo,
    rollover_type character varying(3) ENCODE lzo,
    rollover_amt numeric(38,10) ENCODE az64,
    princ_liq_branch character varying(9) ENCODE lzo,
    next_maturity_date timestamp without time zone ENCODE az64,
    book_ccy character varying(9) ENCODE lzo,
    has_drcr_adv character varying(3) ENCODE lzo,
    rd_flag character varying(3) ENCODE lzo,
    rd_auto_pmnt_takedown character varying(3) ENCODE lzo,
    rd_move_mat_to_unclaimed character varying(3) ENCODE lzo,
    rd_move_funds_on_ovd character varying(3) ENCODE lzo,
    rd_takedown_days integer ENCODE az64,
    rd_takedown_months integer ENCODE az64,
    rd_takedown_years integer ENCODE az64,
    rd_payment_acc character varying(60) ENCODE lzo,
    rd_payment_brn character varying(9) ENCODE lzo,
    rd_payment_ccy character varying(9) ENCODE lzo,
    rd_installment_amt numeric(38,10) ENCODE az64,
    rd_pay_schdt timestamp without time zone ENCODE az64,
    charge_book_brn character varying(9) ENCODE lzo,
    charge_book_acc character varying(60) ENCODE lzo,
    charge_book_ccy character varying(9) ENCODE lzo,
    override_amt_block character varying(3) ENCODE lzo,
    chg_start_date timestamp without time zone ENCODE az64,
    bvt_date timestamp without time zone ENCODE az64,
    combvt_date timestamp without time zone ENCODE az64,
    tenor_code character varying(30) ENCODE lzo,
    auto_extension character varying(3) ENCODE lzo,
    liquidation_amt numeric(38,10) ENCODE az64,
    last_rollover_date timestamp without time zone ENCODE az64,
    allow_prepayment character varying(3) ENCODE lzo,
    interest_rate numeric(38,10) ENCODE az64,
    maturity_amount numeric(38,10) ENCODE az64,
    intrate_cumamt_reqd character varying(3) ENCODE lzo,
    intrate_cumamt_roll_reqd character varying(3) ENCODE lzo,
    roll_tenor_pref character varying(3) ENCODE lzo,
    orig_tenor_days integer ENCODE az64,
    orig_tenor_months smallint ENCODE az64,
    orig_tenor_years smallint ENCODE az64,
    roll_tenor_days integer ENCODE az64,
    roll_tenor_months smallint ENCODE az64,
    roll_tenor_years smallint ENCODE az64,
    dep_tenor_pref character varying(3) ENCODE lzo,
    cascade_month character varying(3) ENCODE lzo,
    add_funds character varying(3) ENCODE lzo,
    additional_amt numeric(38,10) ENCODE az64,
    mat_adv_date timestamp without time zone ENCODE az64,
    redm_int_payout character varying(3) ENCODE lzo,
    process_no numeric(38,10) ENCODE az64,
    id character varying(192) NOT NULL ENCODE raw distkey,
    PRIMARY KEY (id),
    year_key character varying(4),
    month_key character varying(6),
    day_key character varying(8),
    update_date date , 
    row_hash character varying(50)
)
```
----------------

### Creating table actb_udevals

- glue - HO4_actb_udevals_fully
- Source - SFCUBS.ICTB_UDEVALS
- glue db - datalake-processed-kbzrptdcpdb
- glue table - dev_sfcubs_ictb_udevals_daily 

### In Redshift 
- Source - dl_processed_kbzrptdcpdb.dev_sfcubs_ictb_udevals_daily 
- Dest - test_cbs.dev_ictb_udevals


### Creating table 
```bash

CREATE TABLE test_cbs.dev_ictb_udevals (
    prod character varying(12) ENCODE bytedict,
    cond_type smallint ENCODE az64,
    cond_key character varying(69) ENCODE lzo,
    ude_id character varying(48) ENCODE bytedict,
    ude_eff_dt timestamp without time zone ENCODE az64,
    amt numeric(38,10) ENCODE az64,
    rate numeric(38,10) ENCODE az64,
    rate_code character varying(30) ENCODE lzo,
    rate_ccy character varying(9) ENCODE lzo,
    ude_dt timestamp without time zone ENCODE az64,
    rate_dt timestamp without time zone ENCODE az64,
    ude_variance numeric(38,10) ENCODE az64,
    id character varying(192) NOT NULL ENCODE raw distkey,
    process numeric(38,10) ENCODE az64,
    PRIMARY KEY (id),
    year_key character varying(4),
    month_key character varying(6),
    day_key character varying(8),
    rowhash character varying(50)  
)
```

### Serverless udevals
- dev table - hol.dev_ictb_udevals_08_apr_previous


--------------------------------------

### create table test_cbs.dev_ictb_udevals_update

- glue db - dl_processed_kbzrptdcpdb
- glue table - dev_sfcubs_ictb_udevals_daily_update
- dest - test_cbs.dev_ictb_udevals_update 


### Serverless test_cbs.dev_ictb_udevals_update
- dev table - hol.dev_ictb_udevals_08_apr_previous
- dev table - hol.dev_ictb_udevals_update

------------------

## Ictm kbz
```bash

UNLOAD ('SELECT * FROM test_cbs.dev_ictm_acc')
TO 's3://acoe-datalake/dev/raw/ictm_acc_27_apr/'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
FORMAT AS PARQUET;

```

### Remark
- I changed the logic to full refresh becu of complex of logic and data is missmatch


-------------- 

## Ictm_acc serverless
```bash
CREATE TABLE hol.dev_ictm_acc_21_apr_2025 ( brn character varying(9) ENCODE lzo, 
acc character varying(60) ENCODE lzo, calc_acc character varying(60) ENCODE lzo, 
book_acc character varying(60) ENCODE lzo, has_is character varying(3) ENCODE lzo, 
int_start_date timestamp without time zone ENCODE az64, last_is_date timestamp without time zone ENCODE az64, acc_type character varying(3) ENCODE lzo, 
book_brn character varying(9) ENCODE lzo, auto_rollover character varying(3) ENCODE lzo, close_on_maturity character varying(3) ENCODE lzo, 
move_int_to_unclaimed character varying(3) ENCODE lzo, move_pric_to_unclaimed character varying(3) ENCODE lzo, 
maturity_date timestamp without time zone ENCODE az64, princ_liq_ac character varying(60) ENCODE lzo, rollover_type character varying(3) ENCODE lzo, 
rollover_amt numeric(38,10) ENCODE az64, princ_liq_branch character varying(9) ENCODE lzo, next_maturity_date timestamp without time zone ENCODE az64, 
book_ccy character varying(9) ENCODE lzo, has_drcr_adv character varying(3) ENCODE lzo, rd_flag character varying(3) ENCODE lzo, 
rd_auto_pmnt_takedown character varying(3) ENCODE lzo, rd_move_mat_to_unclaimed character varying(3) ENCODE lzo, 
rd_move_funds_on_ovd character varying(3) ENCODE lzo, rd_takedown_days integer ENCODE az64, rd_takedown_months integer ENCODE az64, 
rd_takedown_years integer ENCODE az64, rd_payment_acc character varying(60) ENCODE lzo, rd_payment_brn character varying(9) ENCODE lzo, 
rd_payment_ccy character varying(9) ENCODE lzo, rd_installment_amt numeric(38,10) ENCODE az64, rd_pay_schdt timestamp without time zone ENCODE az64, 
charge_book_brn character varying(9) ENCODE lzo, charge_book_acc character varying(60) ENCODE lzo, charge_book_ccy character varying(9) ENCODE lzo, 
override_amt_block character varying(3) ENCODE lzo, chg_start_date timestamp without time zone ENCODE az64, bvt_date timestamp without time zone ENCODE az64, 
combvt_date timestamp without time zone ENCODE az64, tenor_code character varying(30) ENCODE lzo, auto_extension character varying(3) ENCODE lzo, 
liquidation_amt numeric(38,10) ENCODE az64, last_rollover_date timestamp without time zone ENCODE az64, allow_prepayment character varying(3) ENCODE lzo, 
interest_rate numeric(38,10) ENCODE az64, maturity_amount numeric(38,10) ENCODE az64, intrate_cumamt_reqd character varying(3) ENCODE lzo, 
intrate_cumamt_roll_reqd character varying(3) ENCODE lzo, roll_tenor_pref character varying(3) ENCODE lzo, orig_tenor_days integer ENCODE az64, 
orig_tenor_months smallint ENCODE az64, orig_tenor_years smallint ENCODE az64, roll_tenor_days integer ENCODE az64, roll_tenor_months smallint ENCODE az64, 
roll_tenor_years smallint ENCODE az64, dep_tenor_pref character varying(3) ENCODE lzo, cascade_month character varying(3) ENCODE lzo, 
add_funds character varying(3) ENCODE lzo, additional_amt numeric(38,10) ENCODE az64, mat_adv_date timestamp without time zone ENCODE az64, 
redm_int_payout character varying(3) ENCODE lzo, process_no numeric(38,10) ENCODE az64, id character varying(192) NOT NULL ENCODE raw distkey, 
PRIMARY KEY (id), year_key character varying(4), month_key character varying(6), day_key character varying(8), update_date date ,  row_hash character varying(50)
)


COPY hol.dev_ictm_acc
FROM 's3://acoe-datalake/dev/raw/ictm_acc_27_apr/'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
FORMAT AS PARQUET;
```







