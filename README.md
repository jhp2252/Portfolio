Jenkinsfile
Deploying a GitHub Project on EC2 Using Jenkins Pipeline

Project Overview

This project demonstrates how to automate the deployment of a static portfolio website hosted on GitHub to an AWS EC2 instance using Jenkins Pipeline and Nginx.

The project implements a simple CI/CD workflow to retrieve source code from GitHub and deploy website files to a web server running on Ubuntu Linux.

Technologies Used

AWS EC2

Ubuntu 24.04 LTS

Git and GitHub

Jenkins

Jenkins Pipeline

Nginx

Rsync

SSH

Architecture

GitHub → Jenkins Pipeline → AWS EC2 → Nginx → Web Browser

Project Objectives

Launch and configure an Ubuntu EC2 instance.

Install Java and Jenkins.

Install and configure Nginx as a web server.

Create a dedicated website deployment directory.

Configure Jenkins to retrieve source code from GitHub.

Automate deployment using a Jenkinsfile.

Verify the deployed website using curl and a web browser.

Troubleshoot common deployment and permission issues.

Project Workflow

Source code is stored in a GitHub repository.

Jenkins retrieves the repository using Git.

The pipeline checks out the latest source code.

The Build stage confirms the static website requires no compilation.

The Deploy stage uses rsync to copy website files to /var/www/portfolio.

Nginx serves the deployed website to visitors.

The deployment is verified using curl and a web browser.

Jenkins Pipeline Stages

1. Checkout

Retrieves source code from the configured GitHub repository.

2. Build

Confirms the static website is ready for deployment without requiring a compilation step.

3. Deploy

Uses rsync to synchronise website files from the Jenkins workspace to the deployment directory.

The pipeline excludes the .git directory and removes outdated destination files when they no longer exist in the source.

Installation and Configuration

Prerequisites

An AWS account.

An Ubuntu EC2 instance.

SSH access to the instance.

A GitHub repository containing the portfolio website.

Jenkins and Nginx installed and configured.

Website Deployment Directory

The website files are deployed to:

/var/www/portfolio

Nginx uses this directory as the document root for the portfolio website.

Jenkins Configuration

Create a Jenkins Pipeline job and configure it to retrieve the Jenkinsfile from the GitHub repository using Pipeline script from SCM.

Run the pipeline and review the Console Output to confirm each stage completes successfully.

Verification

Check the Nginx response:

curl -I http://localhost/

Check the website HTML:

curl http://localhost/index.html

Open the EC2 public IP address in a browser:

http://YOUR-EC2-PUBLIC-IP/

Replace the placeholder with your instance's public IP address.

Troubleshooting

Permission denied: Check ownership and permissions of /var/www/portfolio.

Rsync failure: Confirm rsync is installed and the Jenkins user has the required permissions.

Nginx 404 error: Check the document root, index file and enabled server configuration.

Website inaccessible externally: Check the EC2 security group allows inbound HTTP traffic on port 80.

Jenkins build failure: Review the pipeline Console Output for the exact error.

Security Considerations

Restrict SSH access to trusted IP addresses.

Restrict Jenkins port 8080 to trusted IP addresses or access through a secure management route.

Never commit private keys, passwords or AWS credentials to GitHub.

Store deployment credentials securely.

Keep Ubuntu, Jenkins and installed packages updated.

Expected Outcome

A static portfolio website hosted on GitHub is deployed to an AWS EC2 instance through a Jenkins Pipeline and served by Nginx.

This project demonstrates the core principles of CI/CD, source control, deployment automation and Linux web server administration.

Future Improvements

Configure automatic pipeline triggers when code changes are pushed to GitHub.

Add automated website validation tests.

Configure HTTPS using a domain name and TLS certificate.

Add monitoring and deployment notifications.

Author

Created as a hands-on DevOps project to practise AWS, Linux, GitHub, Jenkins Pipeline and Nginx deployment.
