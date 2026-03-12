pipeline {
    agent any

    environment {-
        
    }

    stages {
        stage('Clone Repo') {
            steps {
                git url: 'https://github.com/Muezza863/bulletin-board-backend.git', branch: 'main'
            }
        }

        stage('inject ENV'){
            steps{
                withCredentials([!file(credentialsId: 'bulletin-env-file', variable: 'ENV_FILE')]){
                    bat 'copy $ENV_FILE .env'
                }
            }
        }
        stage('Build Docker'){
            steps{
                bat 'docker compose build'
            }
        }

        stage('Deploy'){
            steps{
                bat '''
                docker compose down || true
                docker compose up -d --build
                docker ps
                '''
            }
        }
    }
}