pipeline {
    agent any

    environment {
        IMAGE_NAME = 'divyaedara/test-image'
        DOCKER_CREDENTIALS_ID = 'dockerhub'
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/DivyaSaiEdara/cdd_project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}:latest")
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: "${DOCKER_CREDENTIALS_ID}", usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh 'echo $PASSWORD | docker login -u $USERNAME --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.image("${IMAGE_NAME}:latest").push()
                }
            }
        }
    }
}
