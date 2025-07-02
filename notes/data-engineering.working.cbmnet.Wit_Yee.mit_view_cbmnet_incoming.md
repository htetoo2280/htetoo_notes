---
id: etgj95f7m3a1h9vmatptv5a
title: mit_view_cbmnet_incoming
desc: ''
updated: 1751347082780
created: 1751340427311
---


remark - full refresh (current date)
state - etl-cbm-net-incoming-outgoing
source - dbo.view_cbmnet_incoming
connection - cbmnet_mssql
glue - to-processed-mit-view-cbmnet-incoming
dest - cbs.mit_view_cbmnet_incoming
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_incoming/
procedure - "integration".to_cbs_mit_view_cbmnet_incoming()
catalog - "datalake-processed-kbz-analytics"."mit_kbzreps_view_cbmnet_incoming"

```bash

CREATE TABLE cbs.mit_view_cbmnet_incoming (
    createddatetime character varying(255) ENCODE lzo,
    creationdatetime timestamp without time zone ENCODE az64,
    debtorbankcode character varying(255) ENCODE lzo,
    debtoridenticategory character varying(255) ENCODE lzo,
    debtorbranchcode character varying(255) ENCODE lzo,
    debtorbranchname character varying(255) ENCODE lzo,
    debtoridentification character varying(255) ENCODE lzo,
    debtorname character varying(255) ENCODE lzo,
    creditoridenticategory character varying(255) ENCODE lzo,
    creditorbranchcode character varying(255) ENCODE lzo,
    creditorbranchname character varying(255) ENCODE lzo,
    creditorname character varying(255) ENCODE lzo,
    creditoridentification character varying(255) ENCODE lzo,
    amount numeric(34,2) ENCODE az64,
    charges numeric(34,2) ENCODE az64,
    status character varying(255) ENCODE lzo,
    msgformatid character varying(255) ENCODE lzo,
    transactionid character varying(255) ENCODE lzo,
    reconciliationno character varying(255) ENCODE lzo,
    xref character varying(255) ENCODE lzo,
    cbmnetprocessno character varying(255) ENCODE lzo,
    revcbmprocessno character varying(255) ENCODE lzo,
    instrumentno character varying(255) ENCODE lzo,
    debtorphoneno character varying(255) ENCODE lzo,
    debtoraddress character varying(255) ENCODE lzo,
    creditorphoneno character varying(255) ENCODE lzo,
    creditoraddress character varying(255) ENCODE lzo,
    isreverse character varying(255) ENCODE lzo,
    reasoncode character varying(255) ENCODE lzo,
    eventfundcode character varying(255) ENCODE lzo,
    trnrefno character varying(255) ENCODE lzo,
    extrefnoreq character varying(255) ENCODE lzo,
    trnrefnodailylog character varying(255) ENCODE lzo,
    sourcerefno character varying(255) ENCODE lzo,
    txnid character varying(255) ENCODE lzo,
    year_key character varying(4) ENCODE lzo,
    month_key character varying(6) ENCODE lzo,
    day_key character varying(8) ENCODE lzo
)
DISTSTYLE AUTO;
```
