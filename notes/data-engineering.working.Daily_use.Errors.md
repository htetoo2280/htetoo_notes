---
id: ehtqubuzws2257cuexeq32q
title: Errors
desc: ''
updated: 1762587006431
created: 1757388605639
---


```bush 
date - 20250909
table name - base.kpay_org_detail
fail reason - lenght is not enough
solution - 

ALTER TABLE integration.pay_organization_detail
ALTER COLUMN business_address TYPE VARCHAR(1500);

1. run the left process from step function 
2. run etl daily main
3. run dbt jobs 
4. run dbt manually becu dbt jobs is fail.
```
