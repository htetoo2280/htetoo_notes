---
id: 23hp15636ktzupbdl871o6a
title: S3_to_redshift
desc: ''
updated: 1744087348548
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
```
