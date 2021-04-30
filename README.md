# AWS & EC2 Task

- launch new EC2 ubuntu instance
- research documentation on AWS/Python for python boto3 package to create and manage AWS S3 resources
- set up awscli and python env with required dependencies
- S3 authentication setup with AWS configure on EC2
- create S3 bucket using python-boto3
- upload data/file to S3 bucket using python-boto3
- retrieve content/file from S3 using python-boto3
- delete content from S3 using python-boto3
- delete the bucket using python-boto3

## Process
- set up new instance, ssh in, and run update and upgrade
- `sudo apt-get install python -y` to install python
- `sudo apt-get install python-pip -y` to install pip
- `sudo apt-get install awscli -y` to install awscli
- configure awscli with `aws configure` and enter the keys from the excel file provided at account creation
- `sudo pip install boto3` to install boto3
- `nano README.md` to create a file with some text
- to create a bucket, create a python file and enter the following:
```python
#!/usr/bin/env python
# needed for the file to run right (including the #)

import boto3
s3 = boto3.resource('s3')

s3.create_bucket(Bucket='eng84isobelbucket', CreateBucketConfiguration={'LocationConstraint': 'eu-west-1'})
```
- make the file executable with `sudo chmod +x filename` and run with `./filename`
- to upload a file to the bucket:
```python
s3.meta.client.upload_file('README.md', 'eng84isobelbucket', 'README.md')
# arguments: address of file to upload (/folder/README.md if necessary), bucket name, name on s3
```
- delete file on ec2 with `rm README.md`
- download file from s3 bucket with:
```python
s3.meta.client.download_file('eng84isobelbucket', 'README.md', 'README.md')
# arguments: bucket name, file name on s3, path to file on local host
```
- delete file from bucket:
```python
s3.meta.client.delete_object(
    Bucket='eng84isobelbucket',
    Key='README.md'
)
```
- delete bucket
```python
s3.meta.client.delete_bucket(
    Bucket='eng84isobelbucket'
)
```