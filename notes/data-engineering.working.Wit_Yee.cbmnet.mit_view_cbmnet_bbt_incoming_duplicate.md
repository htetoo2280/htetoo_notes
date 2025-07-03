---
id: 0g3iwzqownb5ckox6uu9mqc
title: mit_view_cbmnet_bbt_incoming_duplicate
desc: ''
updated: 1751528043924
created: 1751524569150
---

remark - full refresh (current date)
glue - to_processed_mit_view_cbmnet_bbt_incoming_duplicate
connection - cbmnet_mssql
source - dbo.view_cbmnet_bbt_incoming_duplicate
s3 - s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_bbt_incoming_duplicate/
catalog - mit_view_cbmnet_bbt_incoming_duplicate
procedure - "integration".to_cbs_mit_view_cbmnet_bbt_incoming_duplicate()
dest - cbs.mit_view_cbmnet_bbt_incoming_duplicate
stete - etl-cbs-rptdbsrv

*** no data (03/07/25)

