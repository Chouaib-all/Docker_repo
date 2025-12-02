pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-print-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                // Fetch code from GitHub
                git 'https://github.com/ton-utilisateur/MonApp.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }

        stage('Run Container') {
            steps {
                script {
                    // Remove old container if it exists
                    sh 'docker rm -f python-print-app || true'

                    // Run the new container
                    sh 'docker run --name python-print-app ${IMAGE_NAME}'
                }
            }
        }

    }

    post {
        success {
            echo 'Pipeline terminé avec succès !'
        }
        failure {
            echo 'Pipeline échoué.'
        }
    }
}
