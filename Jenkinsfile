pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pratik-Pardeshi/Project-5-Devops.git'
            }
        }

        stage('Build') {
            steps {
                script {
                    def app = docker.build("pratikp02/my-webapp:${env.BUILD_ID}")
                }
            }
        }

        stage('Test') {
            steps {
                sh 'echo Running Tests'
                // Add your test commands here
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('', 'dockerhub-credentials') {
                        app.push()
                    }
                }
                sh 'docker run -d -p 80:80 pratikp02/my-webapp:${env.BUILD_ID}'
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
