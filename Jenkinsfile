pipeline {
    agent any // Artinya: Jalankan di komputer mana saja yang ada Jenkins-nya

    stages {
        // Tahap 1: Ambil kode terbaru dari Git
        stage('Ambil Kode') {
            steps {
                git 'https://github.com/Muezza863/bulletin-board-backend.git'
            }
        }

        // Tahap 2: Buat Image Docker
        stage('Build Image') {
            steps {
                // Jenkins akan menjalankan perintah terminal untuk build docker
                sh 'docker build -t bulletin-board-backend:latest .'
            }
        }

        // Tahap 3: Jalankan Aplikasi
        stage('Run/Deploy') {
            steps {
                // Matikan container lama (jika ada) dan jalankan yang baru
                sh 'docker stop bulletin-board-backend || true'
                sh 'docker rm bulletin-board-backend || true'
                sh 'docker run -d --name bulletin-board-backend -p 80:3000 bulletin-board-backend:latest'
            }
        }
    }
}

// TEST PERUBAHANNNN