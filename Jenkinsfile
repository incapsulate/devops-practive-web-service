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
                    docker.withRegistry("https://${env.AWS_ECR_URL}", 'ecr:us-east-2:aws-user') {
                        def customImage = docker.build("${env.AWS_ECR_URL}/web-service:latest", "-f Dockerfile-web .")

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
//                     kubernetesDeploy(configs: "hellowhale.yml", kubeconfigId: "mykubeconfig")
                }
                echo 'Deploying...'
            }
        }
    }
}