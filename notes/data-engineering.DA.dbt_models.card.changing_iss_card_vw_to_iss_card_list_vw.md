---
id: 8h3yfi86h94qrufwc4cibax
title: changing_iss_card_vw_to_iss_card_list_vw
desc: ''
updated: 1772680885248
created: 1772638895722
---

## in iss_card_vw(old) not having in new
- card_number 
- emboss_name (shorter name because of card length limit)
- last_change_date 

## in iss_card_list_vw(new) not having columns in old
- card_bin 
- card_name 
- id (this is mean cbs account product_id)
- account_type (this may relate with account_number)

------- 

## there are duplication in card_number in both tables
- remark - why this is duplicate???
```sql
select * from kbz_analytics.staging.stg_kbz_iss_card_vw
where card_number = '9503051029251234'
  
```

- this may be error after filtered(1 account error) 
- solved (next model use with union not union all)
```sql
select loan_acc ,count(*) from  kbz_analytics.staging.stg_cbs_credit group by loan_acc having count(*) > 1
```

------- 
## checking max_date and count
```sql

select max(reg_date),count(*) from kbz_analytics.staging.stg_kbz_iss_card_vw -- 2651887

select max(reg_date),count(*) from kbz_analytics.staging.stg_cbs_kbz_iss_card_list_vw -- 2650535 --- this is yesterday data

```
- remark1 - new pipeline is not working perfectly
- remark2 - all data is contain in old


## basic on card_id
```sql
select card_id , count(*)  into #old from kbz_analytics.staging.stg_kbz_iss_card_vw group by card_id 

select card_id , count(*) into #new from kbz_analytics.staging.stg_cbs_kbz_iss_card_list_vw group by card_id 

select * from #old where card_id not in (select card_id from #new) -- many data

select * from #new where card_id not in (select card_id from #old) -- no data

select o.*,n.count from #old o left join #new n on o.card_id = n.card_id where o.count <> n.count --- only 1 account is not equal 100005371080

select * from kbz_analytics.staging.stg_kbz_iss_card_vw where card_id = '100005371080'

```





