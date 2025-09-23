pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'master', url: 'https://github.com/MLopezCamp/jk-diecast.git'
            }
        }

        stage('Construir y desplegar con Docker Compose') {
            steps {
                script {
                    sh 'docker compose down'
                    sh 'docker compose up -d --build'
                }
            }
        }
    }
}
