---
id: jqcwt4mpvvikn2icgxjc5ln
title: tran_nostro
desc: ''
updated: 1772614835429
created: 1772504300764
---

- transactions are not having nostro to define dest branch
- use derive.actb_history and cbs.gltm_glmaster 



## checking the below transaction
 - customer tran not having nostro so even can define summation gl , we cant know the dest branch

```sql
select * from derive.actb_history where trn_ref_no = '2600507595950001'
```









