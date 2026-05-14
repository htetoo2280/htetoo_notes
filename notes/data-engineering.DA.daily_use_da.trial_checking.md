---
id: 4v4hrfo15e6cmqumqej9ibl
title: trial_checking
desc: ''
updated: 1778749354308
created: 1778749245281
---

# this is to find error with F06 tri and our tri from customer

```sql


select account,ac_branch,ac_ccy,
sum(credit_lcy)-sum(debit_lcy) cl_amt 
into #mis
from kbz_analytics.cbs.bitb_mis_detail_trial 
where closing_stat ='MISDailyImport-20260514'---- T+1
-- and ac_branch = '027'
group by account,ac_branch,ac_ccy

select top 10 * from #mis
select top 10 * from #new

-- drop table #new

select gl_code ,ac_branch,ac_ccy,sum(lcy_closing) as lcy_closing into #new from 
-- hol_derive.cbs_daily_gl_bal 
kbz_analytics.derive.cbs_daily_gl_bal
where trn_dt = '2026-05-13'
group by gl_code , ac_branch , ac_ccy -- hol_derive.cbs_daily_gl_bal
-- kbz_analytics.derive.cbs_daily_gl_bal


select n.*,m.cl_amt as mis_closing,n.lcy_closing - m.cl_amt from #new n 
left join #mis m on n.gl_code = m.account and n.ac_branch = m.ac_branch and n.ac_ccy = m.ac_ccy
where n.lcy_closing <> m.cl_amt



select *,n.lcy_closing - m.cl_amt  from #mis m left join #new n on 
n.gl_code = m.account and n.ac_branch = m.ac_branch and n.ac_ccy = m.ac_ccy
where n.lcy_closing <> m.cl_amt
```