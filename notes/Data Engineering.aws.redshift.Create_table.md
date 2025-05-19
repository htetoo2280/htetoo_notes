---
id: eq8p1h0h3mkzh9w6qrvu42k
title: Create_table
desc: ''
updated: 1747625933216
created: 1742360490652
---

### Creating table 




| Orginal Column | Orginal Data | O_len | Len+4       | Upper                | Lower                | Rename                     |
|----------------|--------------|-------|-------------|----------------------|----------------------|----------------------------|
| AUTH_CODE      | VARCHAR2     | 6     | =C2+4       | =VLOOKUP(B2,$W$2:$X$4,2,FALSE) | =E2&D2&")"           | =A2&" "&F2&","             | =LOWER(G2)                 | 
| DATA_DATE      | VARCHAR2     | 8     | =C3+4       | =VLOOKUP(B3,$W$2:$X$4,2,FALSE) | =E3&D3&")"           | =A3&" "&F3&","             | =LOWER(G3)                 |


```bash

SELECT column_name, data_type, data_length, nullable ,TABLE_NAME 
FROM all_tab_columns 
WHERE owner = 'LBI_ODS' AND TABLE_NAME = 'T_O_APP_MMQR_MERCH_RECORD'

```