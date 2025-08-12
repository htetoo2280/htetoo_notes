---
id: bh46ywvgupcdomew8a1me0i
title: Column_schema
desc: ''
updated: 1754549153851
created: 1753167503346
---


```bash 

SELECT column_name, data_type, data_length, nullable ,TABLE_NAME 
FROM all_tab_columns 
WHERE owner = 'LBI_ODS' AND TABLE_NAME = 'T_O_APP_MMQR_MERCH_RECORD'

```

```bash 
SELECT 
    column_name, 
    data_type,
    character_maximum_length AS varchar_length,
    numeric_precision AS numeric_precision,
    datetime_precision
FROM INFORMATION_SCHEMA.COLUMNS
WHERE table_schema = 'staging'
  AND table_name = 'cbs_cbmnet_daily_outgoing_chg'
ORDER BY ordinal_position;
```