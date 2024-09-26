pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Clonar el código del repositorio de GitHub
                git branch: 'main', url: 'https://github.com/thomaspufahl/demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Construir la imagen Docker usando Dockerfile en el repo
                script {
                    docker.build('localhost:5000/demo:latest')
                }
            }
        }

        stage('Push to Registry') {
            steps {
                // Subir la imagen Docker al registry local
                script {
                    docker.withRegistry('http://localhost:5000') {
                        docker.image('localhost:5000/demo:latest').push()
                    }
                }
            }
        }
    }

    post {
        always {
            // Limpia las imágenes no necesarias después de la ejecución
            cleanWs()
        }
    }
}
