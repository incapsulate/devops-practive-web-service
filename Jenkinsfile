#!groovy
pipeline {
    agent any
    environment {
        GITHUB_URL = 'https://github.com/incapsulate/devops-practive-web-service'
        AWS_ECR_URL = '482720962971.dkr.ecr.us-east-2.amazonaws.com'
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.withRegistry(${env.AWS_ECR_URL}, 'credentials-id') {
                        def customImage = docker.build("${env.AWS_ECR_URL}/web-service:latest", "-t -f Dockerfile-web .")

                        customImage.push()
                    }
                }

                echo "Building... ${env.GITHUB_URL}"
            }
        }
        stage('Test') {
            steps {
                echo 'Test...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy...'
            }
        }
    }
}