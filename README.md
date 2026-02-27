CI/CD DevOps Project using Jenkins, Docker and AWS
Project Description

In this project, I designed and implemented a complete CI/CD pipeline to automate application build and deployment using Jenkins, Docker, and AWS services.

The application is containerized and deployed to multiple EC2 instances behind an Application Load Balancer to ensure high availability and reliability.

What I Implemented

Configured GitHub repository for source code management

Set up Jenkins server on AWS EC2

Installed and configured required Jenkins plugins

Created Jenkins pipeline using Jenkinsfile

Integrated GitHub Webhook to trigger automatic builds

Built Docker image from application source code

Implemented version-based Docker image tagging using Jenkins build number

Pushed Docker images to DockerHub

Configured secure credentials in Jenkins

Automated deployment to multiple EC2 instances using SSH

Deployed application containers on port 3000

Configured AWS Application Load Balancer

Created Target Group with health checks

Distributed traffic across multiple EC2 instances

Ensured high availability architecture

Tools and Technologies Used

AWS EC2

AWS Application Load Balancer

AWS Target Groups

Jenkins

Git and GitHub

Docker

DockerHub

Linux (Ubuntu)

Jenkins Plugins Used

Git Plugin

GitHub Integration Plugin

Pipeline Plugin

SSH Agent Plugin

Credentials Binding Plugin

CI/CD Workflow

Developer pushes code to GitHub.

GitHub webhook triggers Jenkins automatically.

Jenkins pulls latest code.

Docker image is built and tagged.

Docker image is pushed to DockerHub.

Jenkins connects to EC2 servers using SSH.

Existing container is removed.

New container is deployed.

Application is accessed through Load Balancer.

Architecture Overview

Developer → GitHub → Webhook → Jenkins → Docker Build → DockerHub → EC2 Instances → Application Load Balancer → Users

Key Outcomes

Automated CI/CD pipeline

Zero manual deployment

Multi-server deployment

Load-balanced production setup

Version-controlled container deployment

Secure credential management

Learning Outcome

Through this project, I gained practical experience in:

CI/CD automation

Docker containerization

AWS infrastructure setup

Load balancing configuration

Secure DevOps practices

Production-style deployment architecture Application runs behind Load Balancer.
