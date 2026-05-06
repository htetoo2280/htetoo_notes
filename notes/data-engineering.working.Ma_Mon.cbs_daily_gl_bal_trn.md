---
id: 0kg8ym6uyimgpckw6vhbemd
title: cbs_daily_gl_bal_trn
desc: ''
updated: 1773136164516
created: 1761118977239
---

## this started from 
- staging.ho_op (starter table)
- backups.staging_opening (keep check points)


### this model is taking from carrying opening balance and day-1 transaction
- carrying closing(opening) + net transaction = closing

- use actb_history for day-1 transaction 
- (not take from actb_accbal_history becu this model can missing some balance manual adjustment can be miss out)


### when error 
- need to rerun from backups.staging_opening day by day

```bush
delete from staging.stg_acoe_cbs_staging_opening


insert into staging.stg_acoe_cbs_staging_opening
select * from backups.staging_opening where trn_dt = '2025-08-18'


delete from  derive.cbs_daily_gl_bal_trn where bkg_date > '2025-08-18'

for ($i=1; $i -le 27; $i++) { Write-Output "=== Run $i/27 ==="; dbt run --select stg_acoe_cbs_staging_opening+ } 
```
### checking with 
```bush
select account,ac_branch,ac_ccy,
sum(credit_lcy)-sum(debit_lcy) cl_amt from cbs.bitb_mis_detail_trial 
where closing_stat ='MISDailyImport-20250201'---- T+1
group by account,ac_branch,ac_ccy
```



