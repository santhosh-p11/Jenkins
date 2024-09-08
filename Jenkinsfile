pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub-credentials')  // Reference to the Docker Hub credentials
        DOCKER_IMAGE = 'santhosh/myapp'  // Replace with your Docker Hub repo
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the code repository
                git 'https://github.com/santhosh-p11/Jenkins.git'  // Replace with your GitHub repo
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }

        stage('Login to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    sh "echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // Push the Docker image to Docker Hub
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker images on the Jenkins node
            sh 'docker rmi $DOCKER_IMAGE || true'
        }
    }
}
