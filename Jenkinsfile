pipeline {
    agent any
    
    environment {
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-credentials'
        DOCKERHUB_IMAGE_NAME = 'your_dockerhub_username/flask-app:latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aditya-g18/CICD-pipeline-with-jenkins', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    customImage = docker.build(DOCKERHUB_IMAGE_NAME)
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS_ID) {
                        customImage.push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy step...'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up after the job'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
