---
id: z7rw6leu74g1yelfewn9q9w
title: runtime_stack
desc: 'finding stack slots'
updated: 1773285581206
created: 1773209926611
---


```sql

-- this is slots config summary
SELECT *
FROM stv_wlm_service_class_config
ORDER BY service_class;

--- all running query
select *
from stv_recents
where status = 'Running' order by starttime ;



--- running in default/others
SELECT 
	
    r.userid,r.status,r.duration,
    r.starttime + INTERVAL '6 hours 30 minutes' AS starttime_local , r.user_name ,r.db_name , r.query ,r.pid ,
    i.*
FROM stv_recents r
LEFT JOIN stv_inflight i
    ON r.pid = i.pid
WHERE r.status = 'Running'
ORDER BY r.starttime;

```

## to block
```sql 
SELECT pg_terminate_backend(1073761276);
```
