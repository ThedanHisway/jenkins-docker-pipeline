pipeline {
    agent any

    environment {
        REGISTRY = "danish072001"  // Your Docker Hub username
        IMAGE_NAME = "webapp"
        TAG = "latest"
        WORKDIR = "C:/jenkins-docker-pipeline" // Change path accordingly
    }

    stages {
        stage('Build & Push Docker Image') {
            steps {
                script {
                    bat 'docker build -t %REGISTRY%/%IMAGE_NAME%:%TAG% .'
                    withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                        bat 'docker push %REGISTRY%/%IMAGE_NAME%:%TAG%'
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    bat 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo 'Build, Push & Deploy Successful!'
        }
        failure {
            echo 'Pipeline Failed. Check logs!'
        }
    }
}
