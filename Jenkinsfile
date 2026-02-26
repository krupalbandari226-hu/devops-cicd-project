pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "krupaldevops/devops-app"
        AWS_REGION   = "ap-south-1"   // change to your region
        LB_NAME      = "devops-alb"
        TG_NAME      = "devops-targets"
        SUBNETS      = "subnet-xxxx subnet-yyyy"  // your subnets
        SG_ID        = "sg-xxxx"  // security group allowing port 80
        VPC_ID       = "vpc-xxxx"
    }

    stages {

        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/krupalbandari226-hu/devops-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'krupaldevops',
                    usernameVariable: 'USER',
                    passwordVariable: 'PASS'
                )]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE:latest'
                }
            }
        }

        stage('Deploy to App Servers') {
            steps {
                sh '''
                ssh ubuntu@172.31.7.248 "docker pull $DOCKER_IMAGE:latest && docker rm -f app || true && docker run -d -p 3000:3000 --name app $DOCKER_IMAGE:latest"
                ssh ubuntu@172.31.14.120 "docker pull $DOCKER_IMAGE:latest && docker rm -f app || true && docker run -d -p 3000:3000 --name app $DOCKER_IMAGE:latest"
                '''
            }
        }

        stage('Create Load Balancer (Optional)') {
            steps {
                sh '''
                # Create Target Group
                aws elbv2 create-target-group \
                    --name $TG_NAME \
                    --protocol HTTP \
                    --port 3000 \
                    --vpc-id $VPC_ID \
                    --health-check-path / \
                    --region $AWS_REGION || true

                # Create ALB
                aws elbv2 create-load-balancer \
                    --name $LB_NAME \
                    --subnets $SUBNETS \
                    --security-groups $SG_ID \
                    --scheme internet-facing \
                    --type application \
                    --region $AWS_REGION || true

                # Register Targets
                aws elbv2 register-targets \
                    --target-group-arn $(aws elbv2 describe-target-groups --names $TG_NAME --query 'TargetGroups[0].TargetGroupArn' --output text --region $AWS_REGION) \
                    --targets Id=172.31.7.248 Id=172.31.14.120 \
                    --region $AWS_REGION
                '''
            }
        }
    }
}
