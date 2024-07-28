pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials-id')
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pratik-Pardeshi/Project-5-Devops-dockerized-webapp-deployment.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build('pratikp02/my-webapp:4')
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    docker.image('pratikp02/my-webapp:4').inside {
                        sh 'make test'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.image('pratikp02/my-webapp:4').inside {
                        sh 'make deploy'
                    }
                }
            }
        }
    }
}
