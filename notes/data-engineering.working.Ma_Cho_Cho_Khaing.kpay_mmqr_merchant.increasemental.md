---
id: 1vh6nfd4o6i99qbxo1m3gq0
title: increasemental
desc: ''
updated: 1752661469228
created: 1752462770464
---


```bash
# Read data from HW source
Oracle_source = glueContext.create_dynamic_frame.from_options(
    connection_type="oracle",
    connection_options={
        "useConnectionProperties": "true",
        "dbtable": "lbi_ods.t_o_app_mmqr_merch_record",
        "connectionName": "huawei-oracle-lbi-extract",
        #"hashexpression": "hash_column_name",
        #"hashpartitions": "10",
        #"enablePartitioningForSampleQuery": True,
        "sampleQuery": f"select * from LBI_ODS.t_o_app_mmqr_merch_record WHERE trunc(Create_time) = to_date('{data_date}','yyyyMMdd')"
    },
    transformation_ctx="Oracle_source"
)

```