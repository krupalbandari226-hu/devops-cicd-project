pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "krupaldevops/devops-app1"
    }

    stages {

        stage('Build Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '0488f83c-f210-462a-a5fe-6ebebaca3cb0',
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
                sshagent(['ec2-ssh-key']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.46.179 "
                    docker pull $DOCKER_IMAGE:latest &&
                    docker rm -f app || true &&
                    docker run -d -p 3000:3000 -e ENVIRONMENT=Production --name app $DOCKER_IMAGE:latest
                    "

                    ssh -o StrictHostKeyChecking=no ubuntu@172.31.40.230   "
                    docker pull $DOCKER_IMAGE:latest &&
                    docker rm -f app || true &&
                    docker run -d -p 3000:3000 -e ENVIRONMENT=Production --name app $DOCKER_IMAGE:latest
                    "
                    '''
                }
            }
        }
    }
}

