---
id: 30rygphbas1udsem6o98sq2
title: cbs_raw
desc: ''
updated: 1772614827781
created: 1771904686972
---



- "cbs.actb_history" - transaction table 
- "cbs.actb_accbal_history" - outstanding history


## opening finding from "actb_accbal_history"

- find max date 
```sql
select branch_code ,account ,acc_ccy , max(bkg_date) as max_bkg_date into #max_bkg from cbs.actb_accbal_history where bkg_date <= '2026-01-01'
group by branch_code,account ,acc_ccy
```
- finding the last balance
- by acc_class becu need to define summation_ac

```sql

select bal_hist.*,substring(bal_hist.account, 4, 3) acc_class  into #opening_main from cbs.actb_accbal_history as bal_hist 
inner join #max_bkg as mx 
on bal_hist.account = mx.account and bal_hist.bkg_date  = mx.max_bkg_date and bal_hist.branch_code  = mx.branch_code
and bal_hist.acc_ccy = mx.acc_ccy
where bal_hist.bkg_date  <= '2026-01-01'  ---- optimize filter
```

- now we get all outstanding by account


----- 
## transaction by account class
- acc_class is need becu to define summation GL
```sql
select ac_branch as branch_code,ac_no ,ac_ccy as acc_ccy -- , substring(ac_no, 4, 3) acc_class 
,sum(case when drcr_ind = 'C' then lcy_amount else 0 end) lcy_credit_total
,sum(case when drcr_ind = 'D' then lcy_amount else 0 end) lcy_debit_total
into #temp 
from cbs.actb_history where trn_dt = '2026-02-02'
group by branch_code,ac_no,ac_ccy
```

- now we get all opening and transaction 
- let's join together

```sql
select op.branch_code ,op.account , op.acc_ccy 
,op.acy_closing_bal as acy_opening, op.lcy_closing_bal as lcy_opening
,lcy_credit_total- lcy_debit_total as lcy_net  into #final
from #opening_main op left join #temp t
on op.account = t.ac_no and op.branch_code = t.branch_code
and op.acc_ccy = t.acc_ccy
```

- finding summation ac (cbs.sttm_account_class_status)
```sql

select -- f.* , acs.dr_gl , acs.cr_gl into 
f.branch_code
,f.account
,f.acc_ccy
,f.acc_class
,f.acy_opening
,f.lcy_opening
,f.lcy_net
,f.lcy_opening + isnull(lcy_net,0) as clac_closing
,case 
when f.lcy_opening + isnull(lcy_net,0) >= 0 then cr_gl
when f.lcy_opening + isnull(lcy_net,0) < 0 then dr_gl
end as summation_ac 
into #final1 
from #final f left join 
cbs.sttm_account_class_status acs on f.acc_class = acs.account_class 
where acs.status = 'NORM' and acs.day_key = 20260208
```






