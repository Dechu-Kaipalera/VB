pipeline {
    agent any  // Run on any available agent
    
    environment {
        // Define Docker credentials and repository information
        DOCKER_REGISTRY = "docker.io"         // Docker registry (default for Docker Hub)
        DOCKER_REPO = "rachu114"              // Your Docker Hub username or repository
        DOCKER_IMAGE = "java-sample-app"      // Docker image name
        DOCKER_TAG = "latest"                 // Docker image tag (you can set this to "latest" or any tag)
    }
    
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout the code from the Git repository
                git 'https://github.com/Dechu-Kaipalera/VB.git'  // Replace with your Git repository URL
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    docker.build("${DOCKER_REPO}/${DOCKER_IMAGE}:${DOCKER_TAG}")
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    // Log in to Docker Hub using credentials stored in Jenkins
                    docker.withRegistry('https://docker.io', 'dockerhub_credentials') {
                        // Push the Docker image to Docker Hub
                        docker.image("${DOCKER_REPO}/${DOCKER_IMAGE}:${DOCKER_TAG}").push()
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline executed successfully! The Docker image has been pushed.'
        }
        failure {
            echo 'Pipeline failed! Check the logs for errors.'
        }
    }
}
