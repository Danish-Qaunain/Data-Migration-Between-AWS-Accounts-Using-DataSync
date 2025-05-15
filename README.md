# Data Migration Between AWS Accounts Using DataSync

This guide provides a comprehensive step-by-step process to migrate data between S3 buckets in two different AWS accounts using AWS DataSync. The procedure includes IAM role creation, S3 bucket policy configuration, DataSync location setup, and task execution.

# Prerequisites

- Two AWS accounts (Source and Destination)
- Source S3 bucket in Account A
- Destination S3 bucket in Account B
- DataSync service enabled in both accounts
- Required IAM permissions to create roles and policies

1. Create IAM Role in Destination Account (Account B)

a. Open IAM Console:

Go to IAM console in the destination account.

Click Roles > Create role. Select AWS Service.Choose DataSync.
Click Next.

b. Add Permissions Policy 

c. Use the Destination role inline policy 

d. Save the role ARN for later use.


2. Update Bucket Policy in Source Account 

a. Go to the S3 console in Account A.

b. Navigate to the source bucket.

c .Add the following  source bucket policy:


4. Update Bucket Policy in Destination Account

a. Go to the S3 console in Account B.

b. Navigate to the Destination bucket.

c. Add the following  Destination bucket policy:


5. Create DataSync Destination Location in Account B
through CLI

The CLI command for creating the DataSync destination location in Account B
  aws datasync create-location-s3 \
  --s3-bucket-arn arn:aws:s3:::destination-bucket-name \
  --subdirectory "/" \
  --s3-storage-class STANDARD \
  --s3-config BucketAccessRoleArn=arn:aws:iam::DESTINATION_ACCOUNT_ID:role/DataSyncDestinationRole


5. Create DataSync Task in Account A

a. Open DataSync console in Account A.

b. Click Create task.

c. Select the source and destination locations.

d. Configure task settings (e.g., include/exclude filters, data verification).

e. Click Create task.


6. Create DataSync Task in Account B

a. Open DataSync console in Account B.

b. Click Create task.

c. Select the source and destination locations.

d. Configure task settings (e.g., include/exclude filters, data verification).

e. Click Create task.


7. Start DataSync Task

a. Go to DataSync console in Account B.

b. Select the task and click Start.

c. Monitor the task progress and verify the data transfer.


8. Post-Migration Verification

Verify data integrity in the destination S3 bucket.
Confirm access and permissions for the migrated data.
