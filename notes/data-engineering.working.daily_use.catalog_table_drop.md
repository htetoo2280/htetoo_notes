---
id: sx94oye481ojozy18x0md4q
title: Catalog_table_drop
desc: ''
updated: 1760077764066
created: 1760074874501
---


## use for drop catalog and recreate table again
```bush
import boto3

# Create Glue client
glue_client = boto3.client('glue')

database_name = "datalake-processed-smartpayprod"
table_name = "h2h_payroll_remittance_master"

try:
    # Delete the existing table
    glue_client.delete_table(
        DatabaseName=database_name,
        Name=table_name
    )
    print(f"Deleted existing table: {table_name}")
except Exception as e:
    print(f"Error deleting table: {str(e)}")

# Your existing job will now create the table with the correct schema including ho_remark
```