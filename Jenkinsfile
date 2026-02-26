pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "krupaldevops/devops-app"
    }

    stages {

        stage('Clone') {
            steps {
               git branch: 'main', url: 'https://github.com/krupalbandari226-hu/devops-cicd-project.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
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
                ssh ubuntu@ 172.31.7.248 "docker pull $DOCKER_IMAGE:latest && docker rm -f app || true && docker run -d -p 3000:3000 -e ENVIRONMENT=Production --name app $DOCKER_IMAGE:latest"
                ssh ubuntu@172.31.14.120 "docker pull $DOCKER_IMAGE:latest && docker rm -f app || true && docker run -d -p 3000:3000 -e ENVIRONMENT=Production --name app $DOCKER_IMAGE:latest"
                '''
            }
        }
    }
}
