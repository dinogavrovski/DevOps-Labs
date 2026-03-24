pipeline {
    agent any
    environment {
        // Replace with your Docker Hub username/repo
        DOCKER_IMAGE = 'diga2k/nginx-homework'
        DOCKER_CREDS = 'docker-hub-credentials-id'
    }
    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE}:${env.BUILD_ID} ."
                }
            }
        }
        stage('Push image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKER_CREDS}") {
                        sh "docker push ${DOCKER_IMAGE}:${env.BUILD_ID}"
                    }
                }
            }
        }
    }
}