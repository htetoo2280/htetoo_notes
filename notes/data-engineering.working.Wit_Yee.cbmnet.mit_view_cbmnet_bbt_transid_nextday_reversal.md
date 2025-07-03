---
id: yp1h2gi7oc8cho8xt88133a
title: mit_view_cbmnet_bbt_transid_nextday_reversal
desc: ''
updated: 1751528293062
created: 1751355357822
---


remark - full refresh (current date)
glue - to-processed-mit-view-cbmnet-bbt-transid-nextday-reversal
source - dbo.View_CBMNET_BBT_TRANSID_NEXTDAY_REVERSAL
connection - cbmnet_mssql
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_bbt_transid_nextday_reversal/
catalog - "datalake-processed-kbz-analytics"."mit_view_cbmnet_bbt_transid_nextday_reversal"
procedure - "integration".to_cbs_mit_view_cbmnet_bbt_transid_nextday_reversal()
dest - etl-cbs-rptdbsrv

state - no data (03/07/25)
