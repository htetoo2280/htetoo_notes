---
id: ehhjvj00wdcue1v9wxtts0o
title: Ibanking_auditlog
desc: ''
updated: 1747018947470
created: 1743999292576
---

- [[data-engineering.working]]

# Email
- email - Re: Request : CBS Objects Deployment in Redshift

rowcount is drop on Mar9 due to integration of corebanking removing rsa login.
so they may request new requirement.

auditlog --- all log table
host_auditlog -- only mobile top up
kbz_api_auditlog -- internal transfer
msttxn --- to check all trantype

-------
### this is one time full refresh
- connection - ibanking-fcubsdr-onperm
- glue - raw-to-processed-auditlog-update
- s3 - kbz_analytics/i-banking/auditlog_update/year_key={year_key}/month_key={month_key}/day_key={day_key}/
- glue db - datalake-processed-fcdbdr
- glue table - auditlog_update_ho


------------------- 

### daily increasemental

- s3 - kbz_analytics/i-banking/auditlog_update/
- glue - raw-to-processed-auditlog-update_daily
- glue db - datalake-processed-fcdbdr
- glue table - auditlog_update_ho


--------------- the process is take too long so i change the following logic

###  auditlog_archive_hist

- glue - auditlog_arcihve_hist
- glue db - datalake-processed-fcdbdr
- glue table -  auditlog_update_archive_hist
- s3 - s3://acoe-datalake-processed/kbz_analytics/i-banking/auditlog_archive_hist/
- source - FCDBADMIN_PRD.AUDITLOG_OFN_6M_NEW




### raw-to-processed-auditlog-update_daily

- glue - raw-to-processed-auditlog-update_daily
- glue db - datalake-processed-fcdbdr
- glue table - auditlog_update_daily
- s3 - s3://acoe-datalake-processed/kbz_analytics/i-banking/auditlog_update_daily/
- stro_to_process - integration.sp_to_cbs_auditlog() 

### checking union all of redshift
```bash

select DD , sum(Cout) from (
select trunc(DATTXNSTART) DD,count(*) Cout from dl_processed_fcdbdr.auditlog_update_archive_hist group by trunc(DATTXNSTART) 
union all
select trunc(DATTXNSTART) DD,count(*) Cout from dl_processed_fcdbdr.auditlog_update_daily 
-- where trunc(DATTXNSTART) >= '20250411'
group by trunc(DATTXNSTART)
)aa group by DD order by DD


select trunc(DATTXNSTART),count(*) from cbs.auditlog group by trunc(DATTXNSTART) order by trunc(DATTXNSTART)

select trunc(execution_start_date),count(*) from derive.ibanking_daily_log group by trunc(execution_start_date)
order by trunc(execution_start_date)

```

### Creating table 
```bash 

CREATE TABLE cbs.auditlog (
idseq numeric(38,2) ENCODE az64,
    idlang character(12) ENCODE lzo,
    iddevice character(8) ENCODE lzo,
    idapp character(8) ENCODE lzo,
    idtxn character(12) ENCODE lzo,
    numsequence character(8) ENCODE lzo,
    iduser character varying(80) ENCODE lzo,
    dattxn TIMESTAMP ENCODE az64,
    txndesc character varying(8000) ENCODE lzo,
    returncode numeric(38,2) ENCODE az64,
    errorcode character varying(80) ENCODE lzo,
    auditrequest  varchar(10),
    auditresponse  varchar(10),
    idcust character varying(120) ENCODE lzo,
    remoteaddress character varying(200) ENCODE lzo,
    idsession character varying(200) ENCODE lzo,
    flgprocessed character(4) ENCODE lzo,
    idrequest character varying(40) ENCODE lzo,
    usertype character varying(20) ENCODE lzo,
    "identity" character varying(20) ENCODE lzo,
    idchanneluser character varying(1020) ENCODE lzo,
    idselected character varying(80) ENCODE lzo,
    dattxnstart TIMESTAMP ENCODE az64,
    idjvm character varying(40) ENCODE lzo,
    sourceaddress character varying(200) ENCODE lzo,
    hdr_referrer character varying(8000) ENCODE lzo,
    hdr_useragent character varying(8000) ENCODE lzo,
    hdr_acceptlang character varying(8000) ENCODE lzo,
    hdr_xfwdfor character varying(8000) ENCODE lzo,
    hdr_os character varying(8000) ENCODE lzo,
    hdr_acceptencoding character varying(8000) ENCODE lzo,
    log_hash character varying(224) ENCODE lzo,
    year_key character varying(4) ENCODE lzo,
    month_key character varying(6) ENCODE lzo,
    day_key character varying(8) ENCODE lzo
)
DISTSTYLE AUTO;
```


### to select from oracle
```bash

SELECT DD , sum(Cout) FROM (
SELECT trunc(DATTXNSTART) DD,count(*) Cout FROM  --- 302183
FCDBADMIN_PRD.AUDITLOG_OFN_6M_NEW 
-- WHERE trunc(DATTXNSTART) = TO_DATE('20250424','YYYYMMDD')  
GROUP BY trunc(DATTXNSTART)
UNION ALL
SELECT trunc(DATTXNSTART) DD,count(*) Cout FROM  --- 1969
FCDBADMIN_PRD.AUDITLOG 
-- WHERE trunc(DATTXNSTART) = TO_DATE('20250424','YYYYMMDD')
GROUP BY trunc(DATTXNSTART) )
aa GROUP BY DD
ORDER BY DD
```


### derive.auditlog

Create table
``` bash
create table derive.auditlog (
idcust character varying(120) ENCODE lzo distkey,
idseq numeric(38,2) ENCODE az64,
iddevice character(8) ENCODE lzo,
ibanking_user_id character varying(80) ENCODE lzo,
execution_start_datetime timestamp without time zone ENCODE az64,
execution_start_date date,
execution_datetime timestamp without time zone ENCODE az64,
execution_date date,
txttype character(12) ENCODE lzo )
```

#### query
``` bash
select  idcust
	   ,idseq
	   ,iddevice
	   ,iduser as ibankig_user_id
	   ,DATTXNSTART as execution_start_datetime
	   ,DATTXNSTART :: date as execution_start_date
	   ,DATTXN as execution_datetime
	   ,DATTXN :: date as execution_date
	   ,IDTXN as txttype
from cbs.auditlog
where DATTXNSTART :: date = current_date :: date - 1
```

- stro - integration.sp_to_derive_ibanking_daily_log()
- source - cbs.auditlog
- dest - derive.ibanking_daily_log



--------------------- 

# AUDITLOG_OFN_6M

- remark - they want to add also AUDITLOG_OFN_6M

------------------
- mindate - 2024-06-11 00:00:00.000
- maxdate - 2024-12-12 00:00:00.000 ***
remark care on maxdate for duplication


- source - FCDBADMIN_PRD.AUDITLOG_OFN_6M
- glue - auditlog_arcihve_hist2_for_AUDITLOG_OFN_6M
- catalog - datalake-processed-fcdbdr.auditlog_update_archive_hist_auditlog_ofn_6m


