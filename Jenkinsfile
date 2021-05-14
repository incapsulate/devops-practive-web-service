#!groovy
pipeline {
    agent {
        any {

        }
    }
    environment {
        GITHUB_URL = 'https://github.com/incapsulate/devops-practive-web-service'
    }
    stages {
        stage('Build') {
            steps {
                echo "Build... ${env.GITHUB_URL}"
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