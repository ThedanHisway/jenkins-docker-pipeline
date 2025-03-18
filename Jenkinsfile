pipeline {
    agent any

    environment {
        REGISTRY = "danish072001"  // Your Docker Hub username
        IMAGE_NAME = "webapp"
        TAG = "latest"
        WORKDIR = "C:/jenkins-docker-pipeline" // Change this if needed
    }

    stages {
        stage('Build & Push Docker Image') {
            steps {
                script {
                    sh 'docker build -t $REGISTRY/$IMAGE_NAME:$TAG .'
                    withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                        sh 'docker push $REGISTRY/$IMAGE_NAME:$TAG'
                    }
                }
            }
        }

        stage('Deploy Application') {
            steps {
                script {
                    sh 'docker-compose up -d'
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
