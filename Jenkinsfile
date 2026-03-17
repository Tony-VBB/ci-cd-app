pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "<your-dockerhub-username>/<register>_<roll>"
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/<your-username>/ci-cd-app.git'
            }
        }

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