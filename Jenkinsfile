
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Downloading project from GitHub'
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t registration-web:latest .'
            }
        }

        stage('Deploy Using Docker') {
            steps {
                sh '''
                    docker rm -f registration-web || true
                    docker run -d --name registration-web \
                      -p 8081:80 registration-web:latest
                '''
            }
        }
    }
}
