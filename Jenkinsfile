pipeline {
    agent any

    stages {
        // Tahap 1: Ambil kode terbaru dari Git
        stage('Ambil Kode') {
            steps {
                git branch: 'main', url: 'https://github.com/Muezza863/bulletin-board-backend.git'
            }
        }

        // Tahap 2: Buat Image Docker
        stage('Build Image') {
            steps {
                bat 'docker build -t bulletin-board-backend:latest .'
            }
        }

        // Tahap 3: Run/Deploy menggunakan file .env yang disimpan di Jenkins Credentials
        stage('Run/Deploy') {
            steps {
                // withCredentials('secretFiles') memungkinkan kita untuk memakai file rahasia dari Jenkins
                // 'bulletin-env-file' adalah ID Credential di Jenkins tempat Anda mengupload file .env
                withCredentials([file(credentialsId: 'bulletin-env-file', variable: 'ENV_FILE')]) {
                    
                    bat 'docker stop bulletin-board-backend || exit 0'
                    bat 'docker rm bulletin-board-backend || exit 0'

                    // Menggunakan file rahasia yang dimount oleh Jenkins sementara melalui variabel ENV_FILE
                    bat 'docker run -d --name bulletin-board-backend --env-file "%ENV_FILE%" -p 80:3000 bulletin-board-backend:latest'
                }
            }
        }
    }
    post{
        success {
            echo 'Pipeline berhasil!'
        }
        failure {
            echo 'Pipeline gagal!'
        }
    }
}