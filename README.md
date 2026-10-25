# ContentSphere Infrastructure Automation Using Ansible

## Project Overview

This project automates the configuration and deployment of the ContentSphere web server using Ansible. It demonstrates ad-hoc commands, playbooks, variables, Jinja2 templates, reusable roles, and AWS resource automation.

## Technologies Used

- Ansible
- AWS EC2
- AWS S3
- Nginx
- Ubuntu Linux
- YAML
- Jinja2
- Python, Boto3, and Botocore

## Project Structure

```text
ContentSphere-Ansible-Project/
├── README.md
├── inventory
├── setup-webserver.yml
├── deploy-webpage.yml
├── run-webserver-role.yml
├── group_vars/
│   └── webserver.yml
├── handlers/
│   └── main.yml
├── templates/
│   ├── index.html.j2
│   └── contentsphere.conf.j2
├── roles/
│   └── webserver/
│       ├── tasks/main.yml
│       ├── handlers/main.yml
│       ├── vars/main.yml
│       └── templates/
├── playbooks/
│   ├── ec2.yml
│   └── s3.yml
├── files/
│   └── contentsphere-test.txt
├── screenshots/
└── documentation/
    └── Project_Report.pdf
```

## Features Implemented

### 1. Ansible Ad-Hoc Commands
- Checked managed-server connectivity and system information.
- Installed and managed the Nginx service.
- Created files, directories, and a Linux user.
- Applied file permissions.

### 2. Web Server Configuration
- Installed and enabled Nginx.
- Created the application directory.
- Deployed the ContentSphere webpage.
- Verified the webpage using HTTP requests.

### 3. Variables, Templates, and Handlers
- Defined application variables in `group_vars/webserver.yml`.
- Used Jinja2 templates for the HTML page and Nginx configuration.
- Configured a handler to restart Nginx when its configuration changes.

### 4. Reusable Ansible Role
- Organized Nginx installation and configuration tasks into the `webserver` role.
- Added templates and a handler.
- Executed the role and verified the application.

### 5. AWS Automation
- Used an EC2 IAM role for AWS authentication instead of storing long-term access keys.
- Created an EC2 instance with Ansible in `ap-south-1`.
- Created an S3 bucket and uploaded `contentsphere-test.txt`.
- Verified the uploaded object and its contents using AWS CLI.

## Prerequisites

- Ansible installed on the control node.
- SSH connectivity from the control node to the managed Ubuntu server.
- An inventory file configured for the managed host.
- An AWS IAM role or other securely configured AWS credentials with the required permissions.
- The `amazon.aws` Ansible collection, Boto3, and Botocore for AWS automation.

## Running the Playbooks

Check connectivity:

```bash
ansible -i inventory webserver -m ping
```

Configure the web server:

```bash
ansible-playbook -i inventory setup-webserver.yml
```

Deploy the webpage using variables and templates:

```bash
ansible-playbook -i inventory deploy-webpage.yml
```

Run the reusable role:

```bash
ansible-playbook -i inventory run-webserver-role.yml
```

Provision the AWS EC2 instance:

```bash
ansible-playbook playbooks/ec2.yml
```

Create the S3 bucket and upload the test file:

```bash
ansible-playbook playbooks/s3.yml
```

## Verification

The web application was verified by requesting `http://localhost` on the managed server. The returned HTML displayed the ContentSphere Platform title and heading, and Nginx was confirmed running.

The AWS EC2 playbook reported a running instance. The S3 playbook created a bucket, uploaded the test file, and verified the uploaded object. AWS CLI was also used to list and retrieve the test file.

## Screenshots and Report

The `screenshots/` directory is intended for evidence of Ansible installation, connectivity, playbook execution, website deployment, EC2 provisioning, and S3 upload.

Place the final project report at `documentation/Project_Report.pdf`.

## Cleanup

After project evaluation, remove only the AWS resources created for this project if they are no longer required. Delete the uploaded S3 object before deleting its bucket, and terminate the EC2 instance created for the task. Confirm the resource IDs before performing cleanup.

## Conclusion

This project demonstrates infrastructure configuration using Ansible, reusable role design, Jinja2 templating, Nginx deployment, and AWS EC2/S3 automation.
