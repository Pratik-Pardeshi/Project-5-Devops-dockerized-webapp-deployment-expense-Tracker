pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build("pratikp02/my-webapp:4")
                }
            }
        }
        stage('Test') {
            steps {
                sh 'echo Running Tests'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('pratikp02/my-webapp:4').push()
                    }
                }
            }
        }
    }
    post {
        always {
            cleanWs()
            echo 'Cleanup done!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
