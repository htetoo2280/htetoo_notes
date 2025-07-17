---
id: qab5d7ag4ihhfwz5no4i8gz
title: change_to_increasemental
desc: ''
updated: 1752661460686
created: 1750737830621
---

1. t_o_app_mmqr_order: Determine the update based on the creation time and update time.


solution - take full refresh from source table and insert , update in procedure.

```bash

CREATE OR REPLACE PROCEDURE "integration".to_base_kpay_mmqr_order()
 LANGUAGE plpgsql
AS $$
DECLARE

    -- var_max_data_date date;
    var_data_date date;
    var_day_key int;
    
BEGIN
    --- Get max date of incremental COLUMN
    --- incremental column : int_start_date
    -- var_max_data_date :=(select to_date(max(int_start_date),'yyyy-MM-dd') from cbs.ictm_acc);
    

    SELECT dateadd(day, -1, public.f_getdate_mmt())::date INTO var_data_date;
    var_day_key := to_char(var_data_date, 'yyyyMMdd')::int;

    -- delete from cbs.ictm_acc; -- where to_date(int_start_date,'yyyy-MM-dd')=var_max_data_date;


 insert into base.kpay_mmqr_order
 select *  FROM dl_processed.kpay_mmqr_order
 where day_key = var_day_key 
 and trn_order_id not in 
 (select trn_order_id from base.kpay_mmqr_order) ;


-- Update changed records
UPDATE base.kpay_mmqr_order
SET 
--- trn_order_id=source.trn_order_id,  -- primary key 
msg_id=source.msg_id,
trn_time=source.trn_time,
settle_date=source.settle_date,
pay_finished_time=source.pay_finished_time,
priority=source.priority,
trade_type=source.trade_type,
reason_type=source.reason_type,
business_type=source.business_type,
trn_code=source.trn_code,
payer_iden_id=source.payer_iden_id,
payer_iden_value=source.payer_iden_value,
payer_token=source.payer_token,
payer_name=source.payer_name,
payee_iden_type=source.payee_iden_type,
payee_iden_value=source.payee_iden_value,
payee_token=source.payee_token,
payee_name=source.payee_name,
trn_amount=source.trn_amount,
trn_currency=source.trn_currency,
charge_amount=source.charge_amount,
charge_currency=source.charge_currency,
order_type=source.order_type,
link_order_trn_id=source.link_order_trn_id,
refund_total_amount=source.refund_total_amount,
trn_status=source.trn_status,
response_code=source.response_code,
response_message=source.response_message,
remark=source.remark,
batch_no=source.batch_no,
query_count=source.query_count,
create_user=source.create_user,
create_time=source.create_time,
update_user=source.update_user,
update_time=source.update_time,
merchant_order_id=source.merchant_order_id,
cbm_return_status=source.cbm_return_status,
reason_cbm=source.reason_cbm,
cbm_payment_time=source.cbm_payment_time,
total_trn=source.total_trn,
trn_mode=source.trn_mode,
clr_sys_party=source.clr_sys_party,
lcm_instrm_party=source.lcm_instrm_party,
payee_inst_id=source.payee_inst_id,
payment_inst_id=source.payment_inst_id,
end_to_end_id=source.end_to_end_id,
clr_sys_id=source.clr_sys_id,
id=source.id,
ctgy_purp_prtry=source.ctgy_purp_prtry,
trn_settlement_amount=source.trn_settlement_amount,
currency=source.currency,
instd_amt=source.instd_amt,
chrg_br=source.chrg_br,
cdtr_nm=source.cdtr_nm,
payer_id=source.payer_id,
payer_type=source.payer_type,
dbtr_agt_fin_instn_id=source.dbtr_agt_fin_instn_id,
cdtr_agt_fin_instn_id=source.cdtr_agt_fin_instn_id,
cdtr_acct_id=source.cdtr_acct_id,
cdtr_acct_id_type=source.cdtr_acct_id_type,
terminal_id=source.terminal_id,
mcc=source.mcc,
country_code=source.country_code,
merchant_name=source.merchant_name,
city=source.city,
dbtr_nm=source.dbtr_nm,
dbtr_pstl_adr=source.dbtr_pstl_adr,
qr_code=source.qr_code,
next_scan_time=source.next_scan_time,
trn_id=source.trn_id,
refund_trn_id=source.refund_trn_id,
bill_number=source.bill_number,
pre_pay_id=source.pre_pay_id,
refund_request_no=source.refund_request_no,
partition_idx=source.partition_idx,
year_key=source.year_key,
month_key=source.month_key,
day_key=source.day_key
FROM dl_processed.kpay_mmqr_order source
WHERE 
    base.kpay_mmqr_order.trn_order_id = source.trn_order_id
    AND source.day_key = var_day_key
    AND base.kpay_mmqr_order.update_time <> source.update_time;


END;
$$

```



