---
id: liz6rjmh7pokislprs1ks2k
title: max_is_max
desc: ''
updated: 1772636270523
created: 1772636011835
---

- this is finding for max on one column is equal max on other column

## over rownumber but this may duplication on same date

```sql
with ranked as (
    select
        card_number,
        application_id,
        application_date,
        row_number() over (
            partition by card_number
            order by application_id desc
        ) as rn_id,
        row_number() over (
            partition by card_number
            order by application_date desc
        ) as rn_date
    from kbz_analytics.staging.stg_cbs_kbz_app_card_vw
)

select *
from ranked
where rn_id = 1
  and rn_date <> 1
```

## another way is more complete
```sql

  with ranked as (
    select
        card_number,
        application_id,
        application_date,

        -- max values per card_number
        max(application_id) over (partition by card_number) as max_app_id,
        max(application_date) over (partition by card_number) as max_app_date
    from kbz_analytics.staging.stg_cbs_kbz_app_card_vw
)

select *
from ranked
where application_id = max_app_id
  and application_date < max_app_date

```