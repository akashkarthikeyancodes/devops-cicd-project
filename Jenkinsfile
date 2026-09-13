pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-pat',
                    url: 'https://github.com/akashkarthikeyancodes/devops-cicd-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-cicd-app .'
            }
        }

        stage('Login to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region ap-south-1 | \
                docker login --username AWS --password-stdin \
                552072248930.dkr.ecr.ap-south-1.amazonaws.com
                '''
            }
        }

        stage('Push to ECR') {
            steps {
                sh '''
                docker tag devops-cicd-app:latest \
                552072248930.dkr.ecr.ap-south-1.amazonaws.com/devops-cicd-app:latest

                docker push \
                552072248930.dkr.ecr.ap-south-1.amazonaws.com/devops-cicd-app:latest
                '''
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                docker stop devops-cicd-app || true
                docker rm devops-cicd-app || true

                docker pull \
                552072248930.dkr.ecr.ap-south-1.amazonaws.com/devops-cicd-app:latest

                docker run -d -p 80:80 \
                --name devops-cicd-app \
                552072248930.dkr.ecr.ap-south-1.amazonaws.com/devops-cicd-app:latest
                '''
            }
        }
    }
}
