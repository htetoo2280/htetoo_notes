---
id: z9dqbzxykdh08eggsvnq68i
title: Boto3
desc: ''
updated: 1742880447669
created: 1742279747492
---
### Boto3 

- boto3.client is a low-level interface that directly maps to AWS API operations.
- Responses are typically dictionaries or JSON-like structures.
- Use get_paginator for paginated results and get_waiter for waiting on specific states.
- Always handle errors using botocore.exceptions.ClientError.

### learning boto3

```bash
import boto3
s3_client = boto3.client('s3')
```
Purpose:
- Creates a low-level client for the S3 service.
- Allows you to call S3 API operations like list_buckets, get_object, etc.

------------------------------------------

### Listing s3 buckets

```bash
# List all S3 buckets
response = s3_client.list_buckets()

# Print bucket names
for bucket in response['Buckets']:
    print(bucket['Name'])
```
---------------------------------------------

## installing awscli
```bash
pip install awscli
aws configure
```
## Aws access key ID??
- go to IAM row to create user and download access keys.

_______________________________

## error 
File association not found for extension .py
- this is need to change file run application by selecting manual with open with or use the following command

``` bash
ftype Python.File="C:\Users\htetoo.lwin\AppData\Local\anaconda3\envs\my_boto3_env\python.exe" "%1" %*
assoc .py=Python.File
```
- now config is done

------------------------
## Starting boto3

2️⃣ Boto3 Clients vs Resources
Boto3 provides two ways to interact with AWS services:

| Type    | Description                          | Example                     |
|---------|--------------------------------------|-----------------------------|
| Client  | Low-level API (JSON responses)       | `boto3.client("s3")`        |
| Resource| High-level Object-Oriented API       | `boto3.resource("s3")`      |

---------------------

## List all s3 brackets

Understanding for response see the following key-pair-value

{'ResponseMetadata': {'RequestId': 'EA8W865NC7NV07WF''server': 'AmazonS3'}, 'RetryAttempts': 0}, 

'Buckets': [{'Name': 'acoe-datalake-processed-dev', 'CreationDate': datetime.datetime(2025, 3, 20, 4, 53, 16, tzinfo=tzutc())}

- ResponseMetadata is the top level key that contain all data.
- Requestid and Buckets are the keys in Responsemetadata.
- so we cant call print ('Name') directly.

we can call like this 
```bash
import boto3
s3 = boto3.client("s3")
response = s3.list_buckets()
for bucket in response['Buckets']:
    print(bucket['Name'])
```

----------------------------------------

## Creating s3 buckets
```bash

import boto3
# Initialize the S3 client
s3 = boto3.client("s3")

# Specify the bucket name (without 's3://') and file path (object key)
bucket_name = "test-acoe"  # Correct bucket name (no 's3://')
file_path = r"C:\Users\htetoo.lwin\Desktop\working.csv"
object_key = "htet-oo-lwin/boto3_createfile/aa.csv"  # Path inside the bucket

# Upload the file to the specified bucket and object key
s3.upload_file(file_path, bucket_name, object_key)
print(f"File uploaded to {bucket_name}/{object_key}")

```

