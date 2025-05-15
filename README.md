# Data Migration Between AWS Accounts Using DataSync

This guide provides a comprehensive step-by-step process to migrate data between S3 buckets in two different AWS accounts using AWS DataSync. The procedure includes IAM role creation, S3 bucket policy configuration, DataSync location setup, and task execution.

# Prerequisites

- Two AWS accounts (Source and Destination)
- Source S3 bucket in Account A
- Destination S3 bucket in Account B
- DataSync service enabled in both accounts
- Required IAM permissions to create roles and policies

### 1. Create IAM Role in Destination Account (Account B)

a. Open IAM Console:

- Go to IAM console in the destination account.

- Click Roles > Create role. Select AWS Service.Choose DataSync.
- Click Next.

b. Add Permissions Policy 

c. Use the [Destination role inline policy](https://github.com/Danish-Qaunain/Data-Migration-Between-AWS-Accounts-Using-DataSync/blob/main/Destination%20role%20inline%20policy).

d. Save the role ARN for later use.


### 2. Update Bucket Policy in Source Account 

- Go to the S3 console in Account A.

- Navigate to the source bucket.

-  Add the following  [source bucket policy](https://github.com/Danish-Qaunain/Data-Migration-Between-AWS-Accounts-Using-DataSync/blob/main/Source%20bucket%20policy).


### 4. Update Bucket Policy in Destination Account

- Go to the S3 console in Account B.

- Navigate to the Destination bucket.

- Add the following  [Distention Bucket policy](https://github.com/Danish-Qaunain/Data-Migration-Between-AWS-Accounts-Using-DataSync/blob/main/Distention%20Bucket%20policy).


### 5. Create DataSync Destination Location in Account B through CLI

### The CLI command for creating the DataSync destination location in Account B

```
aws datasync create-location-s3 --s3-bucket-arn arn:aws:s3:::Source Bucket Name --s3-storage-class STANDARD --s3-config BucketAccessRoleArn="arn:aws:iam::Destination_Account_ID:role/Your Role Name" --region Your region
```
### 5. Create DataSync Task in Account B

- Open DataSync console in Account B.

- Click Create task.

- Select the source and destination locations.

- Configure task settings (e.g., include/exclude filters, data verification).

- Click Create task.


### 6. Start DataSync Task

- Go to DataSync console in Account B.

- Select the task and click Start.

- Monitor the task progress and verify the data transfer.


### 7. Post-Migration Verification
- Verify data integrity in the destination S3 bucket.
Confirm access and permissions for the migrated data.
