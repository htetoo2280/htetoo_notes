---
id: 9lvmta12nqrnwtauw0fzzui
title: mit_view_cbmnet_outgoing_fp
desc: ''
updated: 1752724358216
created: 1752722362068
---

remark - full refresh (current date)
glue - to-processed-mit-view-cbmnet-outgoing-fp
source - dbo.VIEW_CBMNET_OUTGOING_FP
connection - cbmnet_mssql
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_outgoing_fp/
catalog - "datalake-processed-kbz-analytics"."mit_view_cbmnet_outgoing_fp"
dest - cbs.mit_view_cbmnet_outgoing_fp
procedure - "integration".to_cbs_mit_view_cbmnet_outgoing_fp()
state - etl-cbs-rptdbsrv
