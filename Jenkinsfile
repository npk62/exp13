pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sample-app'
        DOCKER_REGISTRY = 'npk62/sample-app'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'docker run --rm $DOCKER_IMAGE pytest tests/'
            }
        }

        stage('Push to Docker Registry') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials']) {
                    sh 'docker tag $DOCKER_IMAGE $DOCKER_REGISTRY:latest'
                    sh 'docker push $DOCKER_REGISTRY:latest'
                }
            }
        }

        stage('Deploy to Cloud') {
            steps {
                echo 'Deploy to AWS/GCP using Terraform or CLI commands'
            }
        }
    }
}