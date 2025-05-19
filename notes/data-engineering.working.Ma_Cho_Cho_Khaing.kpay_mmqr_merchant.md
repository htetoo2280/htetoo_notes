---
id: oac7csn6t6x80cs77zfja97
title: kpay_mmqr_merchant
desc: ''
updated: 1747627865685
created: 1747626639997
---

- Email - New Table syn up || kpay_mmqr_order


-----------------------------

- state - 
- source - lbi_ods.t_o_app_mmqr_merch_record
- dest - base.kpay_mmqr_merchant
- glue - raw_to_processed_kpay_mmqr_merchant
- procedure - integration.to_base_kpay_mmqr_merchant()
- catalog - dl_processed.mmqr_merchant


```bash
create table base.kpay_mmqr_merchant (
create_time timestamp,
merch_code varchar(64),
merch_name varchar(1024),
merchant_status_mm varchar(64),
merch_pan varchar(64),
company_type_mm varchar(1024),
company_registration_id varchar(512),
merchant_number_mm varchar(1024),
trans_time timestamp,
status varchar(64),
response_message varchar(1024)
)
```