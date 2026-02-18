pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nodejs-3tier-app:%BUILD_NUMBER% .'
            }
        }

        stage('Login to ECR') {
            steps {
                bat '''
                aws ecr get-login-password --region ap-south-1 ^
                | docker login --username AWS --password-stdin 592965056877.dkr.ecr.ap-south-1.amazonaws.com
                '''
            }
        }
    }
}

