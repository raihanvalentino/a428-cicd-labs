pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building React App...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing React App...'
                sh './jenkins/scripts/test.sh'
            }
        }
        // KRITERIA 4: Tambahkan Stage Manual Approval sebelum Deploy
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
            }
        }
        // KRITERIA 2: Deploy Stage
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                
                // KRITERIA 3: Jeda eksekusi otomatis selama 1 menit (60 detik)
                echo 'Aplikasi berhasil di-deploy. Menunggu 1 menit...'
                sleep 60
                
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}