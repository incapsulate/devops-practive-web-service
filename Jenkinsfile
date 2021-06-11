#!groovy
pipeline {
    agent any
    environment {
        GITHUB_URL = 'https://github.com/incapsulate/devops-practive-web-service'
        AWS_ECR_URL = '482720962971.dkr.ecr.us-east-2.amazonaws.com'
        K8S_DEPLOYMENT_NAME = 'web-server'
        DOCKER_IMAGE_NAME = 'web-service'
        SHORT_GIT_COMMIT = sh(returnStdout: true, script: "git log -n 1 --pretty=format:'%h'").trim()
    }
    stages {
        stage('Build') {
            steps {
                script {
                    docker.withRegistry("https://${env.AWS_ECR_URL}", 'ecr:us-east-2:aws-user') {
                        def customImage = docker.build("${env.AWS_ECR_URL}/${env.DOCKER_IMAGE_NAME}:${BUILD_NUMBER}-${env.SHORT_GIT_COMMIT}", "-f Dockerfile-web .")

                        customImage.push()
                    }
                }

                echo "Building... ${env.GITHUB_URL}"
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    sh("kubectl set image deployment/${env.K8S_DEPLOYMENT_NAME} ${env.K8S_DEPLOYMENT_NAME}=${env.AWS_ECR_URL}/${env.DOCKER_IMAGE_NAME}:${BUILD_NUMBER}-${env.SHORT_GIT_COMMIT}");
                }
                echo 'Deploying...'
            }
        }
    }
}