---
id: yb95cok2uhokg5lzivd2ut4
title: Glue_jobs_delete_script
desc: ''
updated: 1757317516836
created: 1757317501590
---

```bush
import boto3
from botocore.exceptions import ClientError


# Initialize Glue client
glue_client = boto3.client('glue')

# List of scripts to delete
jobs_to_delete  = [
'hah_test',
'layer_test',
'my_test',
'adhoc_ait',
    # Add your script names here
]


def delete_glue_jobs(job_names):
    """
    Delete multiple Glue Jobs
    """
    deleted_count = 0
    failed_count = 0
    
    for job_name in job_names:
        try:
            # Delete the Glue Job
            glue_client.delete_job(JobName=job_name)
            print(f"✅ Successfully deleted job: {job_name}")
            deleted_count += 1
            
        except ClientError as e:
            error_code = e.response['Error']['Code']
            if error_code == 'EntityNotFoundException':
                print(f"⚠️ Job not found: {job_name}")
            else:
                print(f"❌ Failed to delete {job_name}: {e}")
                failed_count += 1
        except Exception as e:
            print(f"❌ Error deleting {job_name}: {e}")
            failed_count += 1
    
    print(f"\n📊 Summary: {deleted_count} deleted, {failed_count} failed")

# Run the deletion
delete_glue_jobs(jobs_to_delete)

```