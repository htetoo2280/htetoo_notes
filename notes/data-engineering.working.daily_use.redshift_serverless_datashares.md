---
id: a5p7r6wg51vv56efwoivxh8
title: Redshift_serverless_datashares
desc: ''
updated: 1759467630789
created: 1758168070462
---

## in_dev server share to kbz_analytics_dev
```bush
--if schema is not already added in datashare  
alter datashare dev add schema po;

--show data share 
show datashares;

-- to add a table to datashare
ALTER DATASHARE dev ADD TABLE "po"."derive_Kpay_daily_Wallet_Bal"
-- To remove a table or view from a datashare
ALTER DATASHARE dev REMOVE TABLE "po"."derive_Kpay_daily_Wallet_Bal"
```

## and call in production as following
```bush

select top 10 * from kbz_analytics_dev.test_ksm.test_cbs_mmqr
```


