---
id: w6zoq1vsfubvcrgt7rrr1fy
title: bi_branch_township
desc: ''
updated: 1756789643719
created: 1756117511224
---

- type - full refresh

- step - 
- source -  KBZREPS.BI_BRANCHES_TOWNSHIP
- dest - cbs.bi_branches_township
- glue - ora-processed-kbzreps-bi-branches-township
- connection - core-banking-kbzrptdcpdb-sfcubs
- catalog - datalake-processed-kbz-analytics.bi_branches_township
- proceudre - integration.to_cbs_bi_branches_township()
- remark - 


```bash

create table cbs.bi_branches_township (
cbm_township_code  varchar(80),
smart_branch  varchar(100),
vc_name  varchar(100),
new_territories  varchar(200),
township  varchar(800),
branch_code  varchar(48),
branch_name  varchar(1680),
cbm_reg_code  varchar(200),
cbm_state_code  varchar(80),
cbm_town_code  varchar(80)
)

```