---
id: qab5d7ag4ihhfwz5no4i8gz
title: change_to_increasemental
desc: ''
updated: 1750753756284
created: 1750737830621
---

1. t_o_app_mmqr_order: Determine the update based on the creation time and update time.



## original glue part
```bash

# Read data from HW source
Oracle_source = glueContext.create_dynamic_frame.from_options(
    connection_type="oracle",
    connection_options={
        "useConnectionProperties": "true",
        "dbtable": "LBI_ODS.T_O_APP_MMQR_ORDER",
        "connectionName": "huawei-oracle-lbi-extract",
        #"hashexpression": "hash_column_name",
        #"hashpartitions": "10",
        #"enablePartitioningForSampleQuery": True,
        #"sampleQuery": f"select * from LBI_ODS.T_O_APP_MMQR_ORDER where DATA_DATE = {data_date}"
    },
    transformation_ctx="Oracle_source"
)
```

original is full refresh 

