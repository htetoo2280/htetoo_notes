---
id: rq9vxmn9a11luubn4hr4qw1
title: Auditing_row_checking
desc: ''
updated: 1746500198775
created: 1746500171884
---


## auditing and row count checking
```bash
SELECT DISTINCT ORA_ROWSCN,SCN_TO_TIMESTAMP(ORA_ROWSCN) FROM SFCUBS.ICTB_UDEVALS 
WHERE trunc(UDE_EFF_DT) = TO_DATE('20250505','yyyymmdd') 
AND trunc(SCN_TO_TIMESTAMP(ORA_ROWSCN)) = TO_DATE('20250506','yyyymmdd')
ORDER BY SCN_TO_TIMESTAMP(ORA_ROWSCN)
```