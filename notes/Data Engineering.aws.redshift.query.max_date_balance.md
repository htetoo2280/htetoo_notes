---
id: srcsamqiw8fleap4aw8i53r
title: max_date_balance
desc: ''
updated: 1741330567238
created: 1741329205625
---

can reduce run time more than row number

```bash
#in redshift

select * from ase.cbs_acc_bal_trn t
WHERE (t.acc, t.acc_ccy, t.to_date) IN (    
    SELECT acc, acc_ccy, MAX(to_date)
    FROM base.cbs_acc_bal_trn
    where acc in (select distinct maincode from test_cbs.ho_maincode where remark = 'delete')
    GROUP BY acc, acc_ccy
``` 



```bash
#in oracle

SELECT ACCOUNT , BRANCH_CODE , ACC_CCY ,MAX
(BKG_DATE) AS MAX_BKG_DATE, MAX(LCY_CLOSING_BAL) 
KEEP (DENSE_RANK LAST ORDER BY BKG_DATE) AS 
balance_at_max_date FROM sfcubs.actb_accbal_history 
GROUP BY ACCOUNT , BRANCH_CODE , ACC_CCY 
