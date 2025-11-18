---
id: l2o72h09pc8brqybbnz4kwx
title: Dbt_looping
desc: ''
updated: 1761118953682
created: 1761118933642
---


```bush
for ($i=1; $i -le 27; $i++) { Write-Output "=== Run $i/27 ==="; dbt run --select stg_acoe_cbs_staging_opening+ } 
```