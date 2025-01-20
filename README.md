# Auto Backup of EBS Volume using Snapshot to S3 with the help of AWS CLI

# EBS Snapshot to S3 Backup Script
> This script allows you to create a snapshot of an AWS EBS volume, wait for the snapshot to complete, and    then copy its metadata to an S3 bucket for backup purposes.

Prerequisites
Before running this script, ensure you have the following:

* AWS CLI installed and configured on your local machine or EC2 instance.
* IAM Permissions to create snapshots, describe snapshots, and upload to an S3 bucket.
* A valid EBS Volume ID and S3 Bucket to store the snapshot metadata.

Script Overview
This script performs the following steps:

* Create a Snapshot: It creates a snapshot of the provided EBS volume.
* Wait for Completion: The script waits for the snapshot to finish before proceeding.
* Copy Metadata to S3: It copies the snapshot metadata (not the actual snapshot content) to an S3 bucket in  JSON format.
* Cleanup: The script removes the local metadata file after successfully uploading it to S3.

1. Configure the Script
Open the script and update the following variables:

VOLUME_ID: Replace "vol-xxxxxxxx" with the EBS Volume ID you want to snapshot.
S3_BUCKET: Replace "s3://your-bucket-name" with the S3 bucket you want to store the metadata in.
bash
Copy
Edit
VOLUME_ID="vol-xxxxxxxx"       # Replace with your EBS Volume ID
S3_BUCKET="s3://your-bucket-name"  # Replace with your S3 bucket name

2. Run the Script
Make the script executable:

bash
Copy
Edit
chmod +x snapshot_to_s3.sh
Run the script:

bash
Copy
Edit
./snapshot_to_s3.sh
The script will create the snapshot, wait for it to complete, and then upload the snapshot metadata to your specified S3 bucket.

3. Check the S3 Bucket
Once the script finishes, you should find a JSON file in your S3 bucket with the snapshot metadata. The filename will be the snapshot ID followed by .json (e.g., snap-xxxxxxxx.json).

Example Output
bash
Copy
Edit
Snapshot created: snap-1234567890abcdef0
Waiting for the snapshot to complete...
Snapshot snap-1234567890abcdef0 completed successfully.
Snapshot metadata copied to S3: s3://your-bucket-name/snap-1234567890abcdef0.json
Snapshot process complete.
Notes
Snapshot Size: This script only copies the metadata (e.g., ID, description, and status) of the snapshot to S3. It does not upload the actual data from the snapshot.
IAM Permissions: Ensure that the IAM role or user running the script has permissions for the following actions:
ec2:CreateSnapshot
ec2:DescribeSnapshots
s3:PutObject
ec2:WaitForSnapshotCompleted

License
This project is licensed under the MIT License - see the LICENSE file for details.



