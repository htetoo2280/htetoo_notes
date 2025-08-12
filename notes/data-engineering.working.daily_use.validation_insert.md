---
id: g90b09bs7r85h3870qw2l5k
title: Validation_insert
desc: ''
updated: 1753262686014
created: 1753177095199
---


```bash
UPDATE integration.o11y_validation_config
SET 
src_sql = 'SELECT COUNT(*) AS no_of_record FROM lbi_ods.t_o_app_mmqr_merch_record where TO_CHAR(create_time,''YYYYMMDD'') = TO_CHAR(SYSDATE-1,''YYYYMMDD'') or TO_CHAR(update_time,''YYYYMMDD'') = TO_CHAR(SYSDATE-1,''YYYYMMDD'')' 
, redshift_sql = 'select count(*) as no_of_record from base.kpay_mmqr_merchant where day_key = to_char(f_get_yesterday_mmt(), ''YYYYMMDD'')'
WHERE name = 'kpay_mmqr_merchant'


```