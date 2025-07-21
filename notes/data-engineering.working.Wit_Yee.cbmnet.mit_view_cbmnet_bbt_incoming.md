---
id: 3yolrz8dab7o9faqhu7nx2j
title: mit_view_cbmnet_bbt_incoming
desc: ''
updated: 1752808128822
created: 1751345281062
---


remark - full refresh (current date)
glue - to-processed-mit-view-cbmnet-bbt-incoming
source - dbo.view_cbmnet_bbt_incoming
connection - cbmnet_mssql
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_bbt_incoming/
catalog - "datalake-processed-kbz-analytics"."mit_view_cbmnet_bbt_incoming"
dest - cbs.mit_view_cbmnet_bbt_incoming
procedure - "integration".to_cbs_mit_view_cbmnet_bbt_incoming()

