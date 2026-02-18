pipeline {
    agent any

    environment {
        AWS_REGION = "ap-south-1"
        ACCOUNT_ID = "592965056877"
        ECR_REPO = "592965056877.dkr.ecr.ap-south-1.amazonaws.com/nodejs-3tier-app"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nodejs-3tier-app:%BUILD_NUMBER% .'
            }
        }

        stage('Login to ECR') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'aws-creds',
                    usernameVariable: 'AWS_ACCESS_KEY_ID',
                    passwordVariable: 'AWS_SECRET_ACCESS_KEY'
                )]) {

                    bat '''
                    set AWS_ACCESS_KEY_ID=%AWS_ACCESS_KEY_ID%
                    set AWS_SECRET_ACCESS_KEY=%AWS_SECRET_ACCESS_KEY%
                    aws ecr get-login-password --region ap-south-1 ^
                    | docker login --username AWS --password-stdin 592965056877.dkr.ecr.ap-south-1.amazonaws.com
                    '''
                }
            }
        }

        stage('Tag Image') {
            steps {
                bat 'docker tag nodejs-3tier-app:%BUILD_NUMBER% %ECR_REPO%:%BUILD_NUMBER%'
            }
        }

        stage('Push to ECR') {
            steps {
                bat 'docker push %ECR_REPO%:%BUILD_NUMBER%'
            }
        }
    }
}

