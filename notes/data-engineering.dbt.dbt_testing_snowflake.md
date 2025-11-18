---
id: dnzvnp8vb0nreibimininv8
title: Dbt_testing_snowflake
desc: ''
updated: 1758792497187
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