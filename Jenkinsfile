pipeline {
    agent any

    stages {
        stage('Clonar código') {
            steps {
                git branch: 'master', url: 'https://github.com/MLopezCamp/jk-diecast.git'
            }
        }

        stage('Construir imagen Docker') {
            steps {
                sh 'docker build -t jk-diecast:latest .'
            }
        }

        stage('Desplegar contenedor') {
            steps {
                sh '''
                    docker rm -f jk-diecast || true
                    docker run -d --name jk-diecast -p 8082:80 jk-diecast:latest
                '''
            }
        }
    }
}
