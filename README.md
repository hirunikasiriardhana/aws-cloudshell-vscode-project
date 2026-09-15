# AWS CloudShell & VS Code IDE Project

## Overview
A hands-on project demonstrating the use of **AWS CloudShell** and a cloud-based **VS Code IDE** (code-server) to work with the **AWS CLI** and **Boto3** (AWS SDK for Python). This project covers connecting to AWS compute/dev environments, running AWS CLI commands, executing Python scripts against AWS services, and uploading files to Amazon S3.

## What I did

### 1. AWS CloudShell
- Verified the AWS CLI installation and version
- Listed S3 buckets using the AWS CLI
- Uploaded a Python script (`list-buckets.py`) into CloudShell and ran it using Boto3 to list S3 buckets programmatically
- Split the terminal into multiple panels to compare CLI and SDK output side-by-side
- Copied the script from CloudShell up to an S3 bucket

### 2. VS Code IDE (code-server on EC2)
- Connected to a browser-based VS Code IDE running on an EC2 instance
- Downloaded the script from S3 into the IDE using the AWS CLI
- Hit a `ModuleNotFoundError: No module named 'boto3'` error, then resolved it by installing Boto3 with `pip3`
- Successfully re-ran the script using Boto3
- Created a new `index.html` file directly in the IDE
- Uploaded `index.html` to the S3 bucket using the AWS CLI

## Screenshots

### AWS Management Console
![AWS Console Home]
<img width="1535" height="663" alt="preview (2)" src="https://github.com/user-attachments/assets/07a81c2a-af0d-411d-bcae-3fed4d21a612" />


### VS Code IDE — Project Explorer
![VS Code IDE Explorer]
<img width="1917" height="877" alt="image" src="https://github.com/user-attachments/assets/2402301f-c958-43b2-aae5-17ae9994c6fb" />


### CloudShell — Listing Buckets & Running Boto3 Script
```bash
~ $ aws --version
aws-cli/2.36.42 Python/3.14.6 Linux/6.1.182-227.379.amzn2023.x86_64 exec-env/CloudShell exe/x86_64.amzn.2023

~ $ aws s3 ls
2026-09-15 02:21:44 c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj

~ $ cat list-buckets.py
import boto3
session = boto3.Session()
s3_client = session.client('s3')
b = s3_client.list_buckets()
for item in b['Buckets']:
    print(item['Name'])

~ $ python3 list-buckets.py
c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj

~ $ aws s3 cp list-buckets.py s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj
upload: ./list-buckets.py to s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj/list-buckets.py
```

### VS Code IDE — Installing Boto3 & Uploading index.html
```bash
[ec2-user@ip-10-0-1-13 environment]$ aws s3 ls
2026-09-15 02:21:44 c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj

[ec2-user@ip-10-0-1-13 environment]$ aws s3 cp s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj/list-buckets.py .
download: s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj/list-buckets.py to ./list-buckets.py

[ec2-user@ip-10-0-1-13 environment]$ python3 list-buckets.py
ModuleNotFoundError: No module named 'boto3'

[ec2-user@ip-10-0-1-13 environment]$ sudo pip3 install boto3
...
[ec2-user@ip-10-0-1-13 environment]$ python3 list-buckets.py
c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj

[ec2-user@ip-10-0-1-13 environment]$ aws s3 cp index.html s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj/index.html
upload: ./index.html to s3://c220889a5570634l16836192t1w1000786058-samplebucket-mixbxyg0jxrj/index.html
```

## Files
| File | Description |
|------|-------------|
| `list-buckets.py` | Python script using Boto3 to list all S3 buckets in the account |
| `index.html` | Simple HTML file created in the IDE and uploaded to S3 |

## Skills Demonstrated
- AWS CLI (Command Line Interface)
- AWS SDK for Python (Boto3)
- Amazon S3 (bucket listing, file upload/download)
- Cloud-based development environments (AWS CloudShell, VS Code / code-server on EC2)
- Troubleshooting Python dependency errors (`pip3 install`)

## Notes
This project was built as part of a hands-on AWS training exercise to compare two development environment options — AWS CloudShell (lightweight, terminal-only) and a full VS Code IDE (graphical editor, file browser, integrated terminal) — before choosing a workflow for future cloud development work.
