pipeline {
    agent any

    environment {
        DOCKER_HOST = "tcp://dind:2375"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/MLopezCamp/jk-diecast.git'
            }
        }

        stage('Build Docker image') {
            steps {
                sh 'docker --version'
                sh 'docker build -t jk-diecast:latest .'
            }
        }

        stage('Run container') {
            steps {
                sh 'docker rm -f jk-diecast || true'
                sh 'docker run -d --name jk-diecast -p 8082:80 jk-diecast:latest'
            }
        }
    }
}
