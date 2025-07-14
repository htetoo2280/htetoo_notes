---
id: tydb1jsjf11dgvr7c89pelq
title: kpay_center_agent_tse_mapping
desc: ''
updated: 1751881028150
created: 1751877540697
---

Email - Re: KBZ Pay Center Financial Performance Dashboard (DAC-5869)


``` bash

delete from lookup.kpay_center_agent_tse_mapping ;


create table #kpay_center_agent_tse_mapping (
center_code	 varchar(255),
center_name	 varchar(255),
center_township	 varchar(255),
center_region	 varchar(255),
center_status_start_date	varchar(255), -- 
center_status_end_date	varchar(255), --
operating_hours	 varchar(255),
center_status	 varchar(255),
retail_agent_short_code	 varchar(255),
tse_code	 varchar(255),
super_agent_code	 varchar(255),
super_agent_name	 varchar(255),
agent_tse_operation_start_date	varchar(255), --
agent_tse_operation_end_date	varchar(255), --
employee_id_ri	 varchar(255),
ri_name	 varchar(255)
 )


COPY #kpay_center_agent_tse_mapping
FROM 's3://acoe-datalake-raw/Pay/kpay_center_mapping_csv_manual/Center_Mapping_Format_2025-07-04.csv'
IAM_ROLE 'arn:aws:iam::390295393321:role/acoe-redshift-unload'
CSV
DELIMITER ','
IGNOREHEADER 1 ;


-- insert into real table

insert into lookup.kpay_center_agent_tse_mapping
select 
center_code,
center_name,
center_township,
center_region,
case when center_status_start_date = '-' then null else TO_DATE(center_status_start_date, 'MM/DD/YYYY') end as center_status_start_date,
case when center_status_end_date = '-' then null else TO_DATE(center_status_end_date, 'MM/DD/YYYY') end as center_status_end_date,
operating_hours,
center_status,
retail_agent_short_code,
tse_code,
super_agent_code,
super_agent_name,
case when agent_tse_operation_start_date = '-' then null else TO_DATE(agent_tse_operation_start_date, 'MM/DD/YYYY') end as agent_tse_operation_start_date,
case when agent_tse_operation_end_date = '-' then null else TO_DATE(agent_tse_operation_end_date, 'MM/DD/YYYY') end as agent_tse_operation_end_date,
employee_id_ri,
ri_name from #kpay_center_agent_tse_mapping

```
