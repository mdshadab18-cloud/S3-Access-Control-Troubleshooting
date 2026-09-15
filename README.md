# S3-Access-Control-Troubleshooting
AWS S3 access-control troubleshooting using IAM policies and least-privilege permissions.

# Project Objective

Built a hands-on AWS S3 and IAM troubleshooting lab to understand access control, permissions, and least-privilege access.

The project demonstrates:

- S3 bucket creation and object access
- IAM user permissions
- Read-only S3 access
- AccessDenied troubleshooting
- Custom IAM policy creation
- `s3:PutObject` permission
- Bucket-specific ARN restriction
- Least-privilege access

## AWS Services Used

- Amazon S3
- AWS IAM

## Initial Configuration

The IAM user was assigned:

`AmazonS3ReadOnlyAccess`

This allowed the user to:

- View S3 objects
- Download objects

But uploading objects was denied.

## Troubleshooting Scenario

A test upload was attempted using the IAM user.

The upload failed with an access-denied error.

The IAM policy was reviewed and the missing permission was identified:

```text
s3:PutObject
```

`PutObject` is the S3 permission used to upload an object.

## Resolution

A custom IAM policy named:

`S3-Lab-Accsess`

was created with the required `s3:PutObject` permission.

The permission was restricted to the lab bucket:

```text
arn:aws:s3:::cloud-support-s3-lab-1/*
```

The policy was attached to the IAM user.

## Verification

After the policy was attached:

- S3 object download → Successful
- S3 object upload → Successful

The user was given only the required upload permission instead of full S3 access.

## Troubleshooting Workflow

```text
Upload failed
     ↓
Check IAM permissions
     ↓
Identify missing s3:PutObject
     ↓
Create custom policy
     ↓
Restrict access to specific bucket
     ↓
Attach policy to IAM user
     ↓
Retry upload
     ↓
Upload successful
```

## Key Skills Demonstrated

- Amazon S3
- AWS IAM
- IAM policies
- S3 permissions
- `s3:PutObject`
- ARN resource restriction
- Least-privilege access
- AccessDenied troubleshooting
- Permission troubleshooting
- Cloud support fundamentals

## Security Note

The S3 bucket was kept private.

No passwords, AWS access keys, private keys, or other secrets were added to this repository.
