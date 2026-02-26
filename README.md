# CI/CD DevOps Project

## Project Overview
This project demonstrates a complete CI/CD pipeline using GitHub, Jenkins, Docker, and AWS EC2.

## Architecture
Developer → GitHub → Webhook → Jenkins → Docker → EC2 → Application (Port 3000) → Load Balancer

## Features
- Automated build and deployment
- Docker image pushed to DockerHub
- Deployment to multiple EC2 instances
- Application Load Balancer with health checks
- Rolling deployment strategy
- Environment variables for production

## Tools Used
- AWS EC2
- Jenkins
- Docker
- GitHub
- DockerHub
- Application Load Balancer

## How It Works
1. Developer pushes code to GitHub.
2. GitHub webhook triggers Jenkins.
3. Jenkins builds Docker image.
4. Docker image is pushed to DockerHub.
5. App servers pull latest image.
6. Application runs behind Load Balancer.
