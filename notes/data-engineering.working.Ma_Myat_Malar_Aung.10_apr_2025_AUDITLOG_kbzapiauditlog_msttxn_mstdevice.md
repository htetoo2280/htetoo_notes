---
id: zw7cfofn28aj1i2jy3fee3p
title: 10_apr_2025_AUDITLOG_kbzapiauditlog_msttxn_mstdevice
desc: ''
updated: 1745555861621
created: 1745471468881
---


### Email Title
- CBS Objects Deployment in Redshift
- Date - 10-apr-2025

We would like to request the data pipelines for the following objects to our redshift database.And then it is updated in our CBS objects migration sheet.

1. AUDITLOG
2. kbz_api_auditlog
3. MSTTXN
4. MSTDEVICE

Additionally,one time full upload the archival table AUDITLOG_OFN_6M_NEW and then merged the production table  AUDITLOG so our redshift table will be archival table plus production table.

-------------------

## AUDITLOG

- AUDITLOG is in Ibanking_auditlog

--------------------------------

## kbz_api_auditlog

###  <u>Glue</u>

- source - FCDBADMIN_PRD.kbz_api_auditlog
- glue - raw_to_processed_kbz_api_auditlog
- s3 - s3://acoe-datalake-processed/kbz_analytics/kbz_api_auditlog/
- gluecatelog - datalake_processed_fcdbdr.kbz_api_auditlog
- procedure - integration.sp_to_cbs_kbz_api_auditlog()
- dest - cbs.kbz_api_auditlog

### <u>Creating table</u>

``` bash

create table cbs.kbz_api_auditlog(
referenceno varchar(100),
idrequest varchar(510),
iduser varchar(40),
idchanneluser varchar(510),
idtxn varchar(6),
iddevice varchar(4),
api_request varchar(65000),
api_response varchar(65000),
request_time datetime,
response_time datetime,
status varchar(8),
host_reference_no varchar(100),
year_key varchar(8),
month_key varchar(6),
day_key varchar(4)
)
```

------------------------- 

## MSTTXN

### <u>pileline</u>

- source - FCDBADMIN_PRD.msttxn
- glue - raw_to_processed_msttxn_full
- s3 - s3://acoe-datalake-processed/kbz_analytics/msttxn/
- gluecatelog - datalake_processed_fcdbdr.msttxn
- procedure - integration.sp_to_cbs_msttxn()
- dest - cbs.msttxn

### <u>Creating table</u>

``` bash

create table cbs.msttxn (
idtxn char(6),
description varchar(510),
txngroup varchar(20),
idseq int,
flagservicerequest char(2),
gifname varchar(510),
ismenutxn char(2),
token1 varchar(510),
token2 varchar(510),
token3 varchar(510),
token4 varchar(510),
token5 varchar(510),
idproxyreqd varchar(2),
idapp char(4),
enabletxnblackout varchar(2),
limitsallowed varchar(2),
typecust varchar(40),
codtxn char(8),
idmodule varchar(6),
typetxn char(2),
authparam varchar(12),
adtnl_params varchar(4000),
ref_accttype varchar(20),
proxytxnid char(6),
layout_type varchar(10),
allowed_privileges varchar(40),
isexternal varchar(2),
livehelpmoduleid varchar(20),
year_key varchar(4),
month_key varchar(6),
day_key varchar(8)
)
```

---------------------------------------- 

## MSTDEVICE

- source - FCDBADMIN_PRD.mstdevice
- glue - raw_to_process_mstdevice_full
- s3 - s3://acoe-datalake-processed/kbz_analytics/mstdevice/
- gluecatelog - datalake_processed_fcdbdr.mstdevice
- procedure - integration.sp_to_cbs_mstdevice()
- dest - cbs.mstdevice

### <u>Creating table 

```bash

create table cbs.mstdevice (
iddevice char(4),
namdevice varchar(60),
contenttype varchar(100),
idchannel char(6),
year_key varchar(4),
month_key varchar(6),
day_key varchar(8)
)
```

---------------------------- done
