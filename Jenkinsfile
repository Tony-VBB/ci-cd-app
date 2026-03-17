pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "vbalajibhargav2023bcs0162/2023BCS0162_2023BCS0162"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}")
                }
            }
        }

        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-cred', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
                    sh 'echo $PASS | docker login -u $USER --password-stdin'
                }
            }
        }

        stage('Push Image') {
            steps {
                script {
                    docker.image("${DOCKER_IMAGE}").push()
                }
            }
        }
    }
}