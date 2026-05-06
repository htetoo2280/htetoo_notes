---
id: eyaytea93s66dq7t2vl6rqf
title: cbs_svbo_term_maint
desc: ''
updated: 1773199206373
created: 1773199160597
---

----- summary 

1. this table include terminal_id is online or not .
2. which branch assets the terminal
3. matching with terminal and gl_code
4. term 559 is online now 

--- remark -- if not production table , termianl can change between branch. and also gl_code/

```sql

select top 10 * from cbs.svbo_term_maint

---- count
select count(*) from cbs.svbo_term_maint -- 1073

---- is having duplication on branch
select branch , count(*) from cbs.svbo_term_maint stm group by branch having count(*) > 1 -- having duplicate

branch|count|
------+-----+
361   |    4|
113   |    2|
021   |    5|

select * from cbs.svbo_term_maint where branch = '361'

term_id|term_name                    |cluster_id|term_type|branch|branch_name|term_sub_type|status |address                                   |atm_type|state            |city      |latitude|longitude|gl_code  |denomination|cartridge|record_updated_on      |year_key|month_key|day_key |established_date|
-------+-----------------------------+----------+---------+------+-----------+-------------+-------+------------------------------------------+--------+-----------------+----------+--------+---------+---------+------------+---------+-----------------------+--------+---------+--------+----------------+
13703  |YEDASHE BRANCH               |          |Branch   |361   |YEDASHE    |Branch       |Online |Yaytarshay Branch,Yaytarshay,MMR          |NCR     |007 - Bago Region|Yaytarshay|        |         |100300870|            |         |2026-03-09 21:00:01.000|    2026|   202603|20260309|23-MAY-17       |
90505  |YAENI PAPER MILL (U1)        |          |         |361   |YEDASHE    |             |Offline|Yaeni Paper Mill Industry,Yedashe,Bago,MMR|NCR     |007 - Bago Region|Bago      |        |         |100301308|            |         |2026-03-09 21:00:01.000|    2026|   202603|20260309|14-SEP-22       |
90506  |YAENI PAPER MILL (U2)        |          |         |361   |YEDASHE    |             |Offline|Yaeni Paper Mill Industry,Yedashe,Bago,MMR|NCR     |007 - Bago Region|Bago      |        |         |100301309|            |         |2026-03-09 21:00:01.000|    2026|   202603|20260309|14-SEP-22       |
53701  |TAUNGOO TECHNOLOGY UNIVERSITY|          |         |361   |YEDASHE    |             |Offline|Taungoo Technology University,Taungoo,MMR |NCR     |007 - Bago Region|Taungoo   |        |         |100300506|            |         |2026-03-09 21:00:01.000|    2026|   202603|20260309|03-MAY-16       |

------------------------ online?

select branch , count(*) from cbs.svbo_term_maint where status = 'Online'
group by branch having count(*) > 1  ---- there is duplication on online also

branch|count|
------+-----+
384   |    2|
033   |    2|
258   |    2|
110   |    3|
177   |    3|

------------------------- term_id  

select term_id , count(*) from cbs.svbo_term_maint group by term_id having count(*) > 1  --- there is no duplication on term_id

------------------------- one terminal_id  , one gl with online ??

select term_id , count(gl_code) from cbs.svbo_term_maint group by term_id having count(*) > 1  --- yes 

------------------------- gl_code will also be distinct??

select gl_code , count(*) from cbs.svbo_term_maint group by gl_code having count(*) > 1 --- yes 

select distinct day_key from cbs.svbo_term_maint

select count(*) from cbs.svbo_term_maint where status = 'Online'
```
