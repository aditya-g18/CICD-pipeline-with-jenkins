pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/aditya-g18/CICD-pipeline-with-jenkins', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build('your_dockerhub_username/flask-app:latest')
                }
            }
        }
        stage('Push Docker Image to Registry') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        docker.image('your_dockerhub_username/flask-app:latest').push()
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
