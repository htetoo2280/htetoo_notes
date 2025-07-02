---
id: vddfctgojpobz4vm861tbt2
title: mit-view_cbmnet_transid_nextday_reversal
desc: ''
updated: 1751353201751
created: 1751351527531
---

remark - full refresh (current date)
state - etl-cbs-rptdbsrv
glue - to-processed-mit-view_cbmnet_transid_nextday_reversal
source - dbo.View_CBMNET_TRANSID_NEXTDAY_REVERSAL
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_transid_nextday_reversal/
connection - cbmnet_mssql
catalog - "datalake-processed-kbz-analytics"."mit_view_cbmnet_transid_nextday_reversal"
procedure - "integration".to_cbs_mit_view_cbmnet_transid_nextday_reversal()
dest - cbs.mit_view_cbmnet_transid_nextday_reversal

state - etl-cbs-rptdbsrv