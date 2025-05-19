---
id: p9nmi0o5bncaxxz55dew79z
title: Dbt_pushing
desc: ''
updated: 1746691123792
created: 1746590317299
---

## Creating branch
- git branch (ibanking_user)

## Switch branch
- git switch (ibanking_user)


# Step 1
- Add database to source.yml
- add in staging table or view


## dbt run to creating tables
- dbt run --select +ibanking_user(+)

## git add individually 
- git add (models/bank/dim/full_refresh/ibanking_user.sql)

## deleting branch
- git branch --delete (ibanking_user)