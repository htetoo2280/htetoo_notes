---
id: p0s45d8bou5prl88qtwq5o2
title: cbs_acc_bal_trn SCD type2 to Daily
desc: ''
updated: 1744003556794
created: 1744003505915
---

----- daily 
```bash
with CTE_BAL as 
(
select
    c.TheDate,
    b.acc account_no, 
        b.lcy_bal LcyClosingBal
from Dimension.Calendar c
inner join base.cbs_acc_bal_trn b
on c.TheDate BETWEEN b.from_date and b.to_date
inner join lookup.cbs_acc_class a 
on substring(b.acc,4,3)=a.acc_class
where c.TheDate between '2025-03-01' and '2025-03-31' -- and a.deposit_flag = 'Y'
)
select 
    TheDate,
    sum(LcyClosingBal) LcyClosingBal
from CTE_BAL 
group by TheDate
order by TheDate
```

------------------------------ 

```bash
with cte_bal as 
(
select 
    a.bkg_date,
    a.acc,
    a.lcy_bal month_end_bal,
    a.avg_lcy_bal,
    a.cum_acy_bal cumulative_mth_bal
from "aggregate".cbs_monthly_acc_bal_trn a 
inner join lookup.cbs_acc_class b 
on substring(a.acc,4,3)=b.acc_class
where bkg_date = '2025-03-31' and b.deposit_flag = 'Y'
)
select sum(month_end_bal) month_end_bal,sum(avg_lcy_bal) avg_lcy_bal,sum(cumulative_mth_bal) cumulative_mth_bal
from cte_bal
```