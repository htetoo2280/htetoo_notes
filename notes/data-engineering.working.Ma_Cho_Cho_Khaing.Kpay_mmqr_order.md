---
id: 1iber5198svkfg6thdxwpwb
title: Kpay_mmqr_order
desc: ''
updated: 1750737816603
created: 1746600559353
---
- Email - New Table syn up ||kpay mmqr order


--------------------------

- type - full refresh

- step - huawei-lbiextract-upto-datalake-processed
- source - lbi_ods.t_o_app_mmqr_order 
- dest - base.kpay_mmqr_order
- glue - raw_to_processed_kpay_mmqr_order
- catalog - datalake-processed-kbz-analytics.kpay_mmqr_order
- proceudre - integration.to_base_kpay_mmqr_order()


## Creating table base.kpay_mmqr_order
```bash
create table base.kpay_mmqr_order (
trn_order_id varchar(128),
msg_id varchar(128),
trn_time timestamp,
settle_date timestamp,
pay_finished_time timestamp,
priority varchar(32),
trade_type varchar(512),
reason_type varchar(512),
business_type varchar(64),
trn_code varchar(128),
payer_iden_id varchar(256),
payer_iden_value varchar(128),
payer_token varchar(128),
payer_name varchar(512),
payee_iden_type varchar(256),
payee_iden_value varchar(128),
payee_token varchar(128),
payee_name varchar(256),
trn_amount int,
trn_currency varchar(40),
charge_amount varchar(72),
charge_currency varchar(40),
order_type varchar(128),
link_order_trn_id varchar(128),
refund_total_amount varchar(72),
trn_status varchar(48),
response_code varchar(128),
response_message varchar(2048),
remark varchar(2048),
batch_no varchar(256),
query_count varchar(16),
create_user varchar(256),
create_time timestamp,
update_user varchar(256),
update_time timestamp,
merchant_order_id varchar(128),
cbm_return_status varchar(200),
reason_cbm varchar(1024),
cbm_payment_time timestamp,
total_trn varchar(40),
trn_mode varchar(200),
clr_sys_party varchar(200),
lcm_instrm_party varchar(1024),
payee_inst_id varchar(200),
payment_inst_id varchar(200),
end_to_end_Id varchar(400),
clr_sys_id varchar(400),
id varchar(400),
ctgy_purp_prtry varchar(200),
trn_settlement_amount varchar(1024),
currency varchar(200),
instd_amt varchar(200),
chrg_br varchar(200),
cdtr_nm varchar(256),
payer_id varchar(1024),
payer_type varchar(200),
dbtr_agt_fin_instn_id varchar(200),
cdtr_agt_fin_instn_id varchar(200),
cdtr_acct_id varchar(1024),
cdtr_acct_id_type varchar(200),
terminal_id varchar(2048),
mcc varchar(2048),
country_code varchar(2048),
merchant_name varchar(2048),
city varchar(2048),
dbtr_nm varchar(2048),
dbtr_pstl_adr varchar(2048),
qr_code varchar(8192),
next_scan_time timestamp,
trn_id varchar(128),
refund_trn_id varchar(128),
bill_number varchar(128),
pre_pay_id varchar(256),
refund_request_no varchar(128),
partition_idx varchar(64),
year_key varchar(4),
month_key varchar(6),
day_key varchar(8)
 )
```
