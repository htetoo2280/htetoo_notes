---
id: wvy2ksljhaf4kbhl0ozf70u
title: Summary
desc: ''
updated: 1760065977924
created: 1759912654159
---




# Data Migration Tracking

## Overview

Tracking table migrations from source to destination with status and type.

## Migration Table

| Table Name | Remark | Glue | Dest Table | Status | Type |
|------------|--------|------|-------------|---------|-------|
| H2H_SUPPLIER_REMITTANCE_MASTER |  | h2h-supplier-remittancemaster | cbs.h2h_supplier_remittance_master | done | upd and incre |
| H2H_PAYROLL_REMITTANCE_MASTER |  | h2h-payroll-remittancemaster | cbs.h2h_payroll_remittance_master | no data | upd and incre |
| sp_remittancemaster | already exist |  |  | no need |  |
| H2H_SUPPLIER_REMITTANCE_DETAILS |  | h2h_supplier_remittance_details | cbs.h2h_supplier_remittance_details | done | upd and incre |
| H2H_PAYROLL_REMITTANCE_DETAILS |  | h2h_payroll_remittance_details | cbs.h2h_payroll_remittance_details | no data | upd and incre |
| sp_remittancedetails | already exist |  | smartpay_sp_remittancedetails | no need |  |
| sp_client | already exist |  |  | no need |  |
| SP_BankInfo_VIEW |  | sp_bankInfo_view | cbs.sp_bankInfo_view | done | full |
| SP_ContactInfo_VIEW |  | sp-contactinfo-view | cbs.sp_contactinfo_view | done | full |
| SP_ContactInfo_Phone_VIEW |  | sp-contactinfo-phone-view | cbs.sp_contactinfo_phone_view | done | full |
| h2h_supplier_client_master |  | h2h-supplier-client-master | cbs.h2h_supplier_client_master | done | upd and incre |
| h2h_supplier_client_contact |  | h2h-supplier-client-contact | cbs.h2h_supplier_client_contact | done | upd and incre |
| h2h_payroll_client_master |  | h2h-payroll-client-master | cbs.h2h_payroll_client_master | no data | upd and incre |
| h2h_payroll_client_contact |  | h2h-payroll-client-contact | cbs.h2h_payroll_client_contact | no data | upd and incre |



## Status Summary

- **Completed**: 7 tables
- **No Data**: 4 tables
- **Not Required**: 3 tables

## Migration Types

- **upd and incre**: Update and incremental load
- **full**: Full load
- **(blank)**: Not applicable

