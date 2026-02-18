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

