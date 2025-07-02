---
id: 9un90j9nc3i47qlegqqjn65
title: Glue_header
desc: ''
updated: 1751347096156
created: 1751252400714
---

```bash

%connections 'cbmnet_mssql'
%idle_timeout 2880
%glue_version 5.0
%worker_type G.4X
%number_of_workers 5

import sys
import json
import boto3
from datetime import datetime, timedelta
from zoneinfo import ZoneInfo
from awsglue.transforms import *
from awsglue.utils import getResolvedOptions
from pyspark.context import SparkContext
from awsglue.context import GlueContext
from awsglue.job import Job
from awsglue import DynamicFrame
  
sc = SparkContext.getOrCreate()
glueContext = GlueContext(sc)
spark = glueContext.spark_session
job = Job(glueContext)

# Time helpers
def get_current_date():
    return datetime.now(tz=ZoneInfo("Asia/Yangon"))

def get_day_minus_one():
    return get_current_date() - timedelta(days=1)

def sparkSqlQuery(glueContext, query, mapping, transformation_ctx) -> DynamicFrame:
    for alias, frame in mapping.items():
        frame.toDF().createOrReplaceTempView(alias)
    result = spark.sql(query)
    return DynamicFrame.fromDF(result, glueContext, transformation_ctx)

# Partition values
year_key = get_current_date().strftime("%Y")
month_key = get_current_date().strftime("%Y%m")
day_key = get_current_date().strftime("%Y%m%d")
hour_key = get_current_date().strftime("%Y%m%d%H")
minute_key = get_current_date().strftime("%Y%m%d%H%M")


# bucket_name = 'acoe-datalake-processed'
# prefix = f"kbzrptdcpdb/kbzreps/view_cbmnet_incoming/{year_key}/{month_key}/{day_key}/{hour_key}/{minute_key}/"

bucket_name = 'acoe-datalake-processed'
prefix = f"kbzrptdcpdb/kbzreps/mit_view_cbmnet_incoming/{year_key}/{month_key}/{day_key}/"

s3_client = boto3.client('s3')
paginator = s3_client.get_paginator('list_objects_v2')
for page in paginator.paginate(Bucket=bucket_name, Prefix=prefix):
    for obj in page.get('Contents', []):
        s3_client.delete_object(Bucket=bucket_name, Key=obj['Key'])

# Read data from HW source
Oracle_source = glueContext.create_dynamic_frame.from_options(
    connection_type="sqlserver",
    connection_options={
        "useConnectionProperties": "true",
        "dbtable": "dbo.view_cbmnet_incoming",
        "connectionName": "cbmnet_mssql",
        # "hashexpression": "Amount",
        # "hashpartitions": "10",
        # "enablePartitioningForSampleQuery": True,
        #"sampleQuery": f"""select * from dbo.view_cbmnet_incoming"""
    },
    transformation_ctx="Oracle_source"
)
#  Script to transform the data/ please don't use * and make changes according to your requirements
SqlQuery0 = f""" 
    
 SELECT *,
'{year_key}' as year_key,
'{month_key}' as month_key,
'{day_key}' as day_key
from myDataSource
"""

SQL_mapping= sparkSqlQuery(
    glueContext,
    query=SqlQuery0,
    mapping={'myDataSource': Oracle_source},
    transformation_ctx='SQL_mapping',
)

AmazonS3_node1709569084347 = glueContext.getSink(path="s3://acoe-datalake-processed/kbzrptdcpdb/kbzreps/mit_view_cbmnet_incoming/", connection_type="s3", updateBehavior="UPDATE_IN_DATABASE", 
                                                 partitionKeys=["year_key", "month_key", "day_key"], 
                                                 enableUpdateCatalog=True, transformation_ctx="AmazonS3_node1709569084347")
AmazonS3_node1709569084347.setCatalogInfo(catalogDatabase="datalake-processed-kbz-analytics",catalogTableName="mit_kbzreps_view_cbmnet_incoming")
AmazonS3_node1709569084347.setFormat("glueparquet", compression="snappy")
AmazonS3_node1709569084347.writeFrame(SQL_mapping)
job.commit()
```