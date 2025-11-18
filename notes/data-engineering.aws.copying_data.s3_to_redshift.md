---
id: 23hp15636ktzupbdl871o6a
title: S3_to_redshift
desc: ''
updated: 1759381429701
created: 1742360080484
---

### S3 to redshift directly
```bash

------------------ Redshift to s3

UNLOAD ('SELECT * FROM test_cbs.dev_ictm_acc')
TO 's3://acoe-datalake/dev/raw/previous_data/'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
FORMAT AS PARQUET;

```
``` bash
----------------- s3 to redshift

COPY hol.dev_ictm_acc_06_mar_previous
FROM 's3://acoe-datalake/dev/raw/previous_data/'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
FORMAT AS PARQUET;


-- this is update 

COPY report.PBI_Report_Dictionary 
FROM 's3://acoe-datalake-raw/temp/report_dict/report_dict.csv'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
FORMAT AS CSV
DELIMITER ',' 
QUOTE '"'
IGNOREHEADER 1;

```

-----------------

```bash
COPY #kpay_center_agent_tse_mapping
FROM 's3://acoe-datalake-raw/Pay/kpay_center_mapping_csv_manual/Center_Mapping_Format_2025-07-04.csv'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
CSV
DELIMITER ','
IGNOREHEADER 1 ;

```