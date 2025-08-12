---
id: ppqgj0bs1ucit7fomce8ccm
title: Lambda
desc: ''
updated: 1754468967399
created: 1754466591196
---

## AWS lambda

```bash
import boto3
import paramiko
import os
from io import BytesIO
import json

# Initialize S3 client and Secrets Manager client
s3_client = boto3.client('s3')
secrets_client = boto3.client('secretsmanager')




def lambda_handler(event, context):
    print("Event:", event)      # See trigger data
    print("Context:", vars(context))  # See runtime info

    ## event (fuel)
    SourcePath = event.get("SourcePath")
    TargetFilename = event.get("TargetFilename")
    S3SFTPPrefix = event.get("S3SFTPPrefix")
    Extension = event.get("Extension")
    date_format = event.get("date_format")
    # print([SourcePath,TargetFilename,S3SFTPPrefix,Extension,date_format])

    ## Secret.get from configuration
    #secret = get_secret(secret_name)



    #sftp_host = get_secret('SFTP_HOST')
    #sftp_port = int(get_secret.get('SFTP_PORT', 22))
    #sftp_username = get_secret.get('username')
    #sftp_password = get_secret.get('password')

    #print(sftp_host)
    #print([sftp_host,sftp_port,sftp_username,sftp_password])

    return {"statusCode": 200, "body": "Done!"}
```