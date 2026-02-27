# CI/CD DevOps Project

## Project Overview

This project demonstrates the implementation of a complete CI/CD pipeline using GitHub, Jenkins, Docker, and AWS EC2.  
The application is containerized and automatically deployed to multiple EC2 instances behind an Application Load Balancer.

---

## Architecture

Developer → GitHub → Webhook → Jenkins → Docker → EC2 → Application (Port 3000) → Load Balancer

---

## Key Features

- Automated build and deployment process  
- Docker image versioning using Jenkins build number  
- Docker image pushed to DockerHub  
- Deployment to multiple EC2 instances  
- Application Load Balancer with health checks  
- Rolling deployment strategy  
- Environment variable configuration for production  

---

## Tools and Technologies

- AWS EC2  
- Jenkins  
- Docker  
- GitHub  
- DockerHub  
- Application Load Balancer  
- Linux (Ubuntu)

---

## Jenkins Plugins Used

- Git Plugin  
- GitHub Integration Plugin  
- Pipeline Plugin  
- SSH Agent Plugin  
- Credentials Binding Plugin  

---

## CI/CD Workflow

1. Developer pushes code to GitHub  
2. GitHub webhook triggers Jenkins automatically  
3. Jenkins pulls latest source code  
4. Docker image is built and tagged  
5. Docker image is pushed to DockerHub  
6. Jenkins deploys container to EC2 instances  
7. Load Balancer distributes traffic  

---

## Deployment Details

- Application Port: 3000  
- Load Balancer Listener: Port 80  
- Target Group Health Check: HTTP  
- Two EC2 instances for high availability  

---

## Project Outcome

Successfully built and deployed a production-style CI/CD pipeline with automated deployment, version control, and high availability architecture on AWS.

---
