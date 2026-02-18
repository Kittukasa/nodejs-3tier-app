pipeline {
    agent any

    stages {

        stage('Clone Code') {
            steps {
                git 'https://github.com/Kittukasa/nodejs-3tier-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t nodejs-3tier-app:%BUILD_NUMBER% .'
            }
        }

        stage('List Images') {
            steps {
                bat 'docker images'
            }
        }
    }
}

