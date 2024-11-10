pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'flask-app'
        DOCKER_TAG = 'latest'
        REGISTRY = 'docker.io'    // Docker Hub registry ke liye sahi hai
        REPO = 'aditya1018/flask-app'  // Apne DockerHub username ke saath repo ka naam daalein
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                git branch: 'main', url: 'https://github.com/aditya-g18/CICD-pipeline-with-jenkins.git', credentialsId: 'github-credentials'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image for the Flask app
                    sh 'docker build -t ${REGISTRY}/${REPO}:${DOCKER_TAG} .'
                }
            }
        }

        stage('Push Docker Image to Registry') {
            steps {
                script {
                    // Login to DockerHub
                    withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    }

                    // Push the Docker image to the registry
                    sh 'docker push ${REGISTRY}/${REPO}:${DOCKER_TAG}'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    // Here, you can add steps to deploy the app to your server or cloud.
                    echo 'Deploying the Flask app to the server or cloud environment'
                }
            }
        }
    }

    post {
        always {
            // Cleanup after the job if needed
            echo 'Cleaning up after the job'
        }

        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
