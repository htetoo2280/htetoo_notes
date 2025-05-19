---
id: l7q1g0s20r4g6czbbn13i9z
title: production_ictm_and_udevals
desc: ''
updated: 1746673682053
created: 1746175767808
---


-- Old version backup
### ictm_acc 

- glue - ora-processed-sfcubs-ictm-acc


----------- 
procedure 
{
  "sql": "call integration.to_cbs_ictm_acc()",
  "StatePayload": "Hello from Step Functions!",
  "AWS_STEP_FUNCTIONS_STARTED_BY_EXECUTION_ID.$": "$$.Execution.Id"
}
---------------------- 


### ictm_acc

- source - SFCUBS.ICTM_ACC

- dest - cbs.ictm_acc

- glue - ora-processed-sfcubs-ictm-acc-update-02-may-2025

- s3 - s3://acoe-datalake-processed/kbzrptdcpdb/sfcubs/ictm_acc_update_02_may_2025/

- glue catalog - datalake-processed-kbzrptdcpdb.sfcubs_ictm_acc_update_02_may_2025

- procedure - integration.to_cbs_ictm_acc_update()



--------------------- 

## ictb_udevals

- glue - ora-processed-sfcubs-ictb-udevals-daily-update-05-may-2025
- s3 - s3://acoe-datalake-processed/kbzrptdcpdb/sfcubs/ictb_udevals_daily_update_05_may_2025/
- catalog - dl_processed_kbzrptdcpdb.sfcubs_ictb_udevals_daily_update_05_may_2025
- souce - SFCUBS.ICTB_UDEVALS
- dest - cbs.ictb_udevals
- procedure - integration.to_cbs_ictb_udevals()
