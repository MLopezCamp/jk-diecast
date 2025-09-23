pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Construir imagen con tu Dockerfile
                    sh 'docker build -t jk-diecast:latest .'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                script {
                    // Eliminar contenedor anterior (si existe)
                    sh 'docker rm -f jk-diecast || true'

                    // Correr el contenedor en puerto 8080
                    sh 'docker run -d --name jk-diecast -p 8080:80 jk-diecast:latest'
                }
            }
        }
    }

    post {
        success {
            echo "✅ Despliegue exitoso: abre http://localhost:8080"
        }
        failure {
            echo "❌ Hubo un error en el pipeline, revisa los logs."
        }
    }
}
