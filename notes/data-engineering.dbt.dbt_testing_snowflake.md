---
id: dnzvnp8vb0nreibimininv8
title: Dbt_testing_snowflake
desc: ''
updated: 1787200862026
created: 1754369152856
---

## Setup 1 (snowflake)
- git clone from - jeremyholtzman
jrtests-learn-dbt
- open snowflake account
- change your user name as account admin
- create new warehouse in snowflake
- transfer to the new warehouse
- check the user name is account admin or not and make sure account admin

## dbt commands
```bush
# Run a specific model
dbt run -s my_base_model

# Run all models in a directory
dbt run -s base.*

# Run models with a tag
dbt run -s tag:base

# Run multiple models
dbt run -s model1 model2

# Run model and its children
dbt run -s my_base_model+

# Run model and its parents
dbt run -s +my_base_model

# If you want to see detailed logs
dbt run -s your_base_model_name --debug
```

- create user in snow flake and grant access admin level
- create new warehouse

```sql
GRANT MODIFY ON DATABASE ANALYTICS TO ROLE ACCOUNTADMIN;
GRANT MODIFY ON DATABASE ANALYTICS TO ROLE TRANSFORM_USER;

GRANT USAGE ON WAREHOUSE TRANSFORM_WH TO ROLE TRANSFORM_USER;
GRANT CREATE TABLE ON SCHEMA analytics.public TO ROLE transform_user;
GRANT CREATE VIEW ON SCHEMA analytics.public TO ROLE transform_user;
GRANT CREATE TABLE ON SCHEMA analytics.public TO ROLE transform_user;
GRANT CREATE VIEW ON SCHEMA analytics.public TO ROLE transform_user;

grant create schema on database analytics to role transform_user;
grant usage on all schemas in database analytics to role transform_user;
grant usage on future schemas in database analytics to role transform_user;  
grant select on all tables in database analytics to role transform_user;   
grant select on future tables in database analytics to role transform_user;  
grant select on all views in database analytics to role transform_user;   
grant select on future views in database analytics to role transform_user;
```

## env reload (dbt)
- run when changing in any config
```sql
.\load-env.ps1
```

## in .env file config
```sql
SNOWFLAKE_ACCOUNT=WUIZBPQ-RY17538
SNOWFLAKE_USER=TRANSFORM_USER
SNOWFLAKE_PASSWORD=adLN@2PgRhmJx!m
SNOWFLAKE_ROLE=TRANSFORM_USER
SNOWFLAKE_WAREHOUSE=TRANSFORM_WH
SNOWFLAKE_DATABASE=analytics
SNOWFLAKE_SCHEMA=public
```
- remark - schema is public now so we need to config in macro

## in macro named get_custom_schema
```sql
{% macro generate_schema_name(custom_schema_name, node) -%}
    {%- if custom_schema_name is none -%}
        {{ target.schema }}
    {%- else -%}
        {{ custom_schema_name | trim }}
    {%- endif -%}
{%- endmacro %}
```




## profile.yml
```sql
jrtests_learn_dbt:
  target: dev
  outputs:
    dev:
      type: snowflake
      account: "{{ env_var('SNOWFLAKE_ACCOUNT') }}"
      user: "{{ env_var('SNOWFLAKE_USER') }}"
      password: "{{ env_var('SNOWFLAKE_PASSWORD') }}"
      role: "{{ env_var('SNOWFLAKE_ROLE') }}"
      warehouse: "{{ env_var('SNOWFLAKE_WAREHOUSE') }}"
      database: "{{ env_var('SNOWFLAKE_DATABASE') }}"
      schema: "{{ env_var('SNOWFLAKE_SCHEMA') }}"
      threads: 1
  target: dev
```




## project.yml
- remark - +schema: schema_name
- upper folder and lower folder are optional
```sql
# in project.yml
# Configuring models
models:
  # no schema binding for non-production environments, to resolve external relations
  +bind: "{{ (target.name == 'prod') | as_bool }}"  (option)
  dbt_kbz_analytics: (project name)
    bank: (upper folder) (option)
      derive: (lower folder) (option)
        incremental: (folder)
          +schema: derive (real schema)
          +materialized: "{{ 'incremental' if target.name in ['prod', 'uat'] else 'view'}}"
        full_refresh: (folder)
          +schema: derive  (real schema)
          +materialized: "{{ 'table' if target.name in ['prod', 'uat'] else 'view'}}" 
        view: (folder)
          +schema: derive (real schema)
          +materialized: view
          
```

