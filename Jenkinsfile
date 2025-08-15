pipeline {
    agent any

    environment {
        // Replace 'dockerhub-credentials-id' with the ID of your Docker Hub credentials in Jenkins
        DOCKERHUB_CREDENTIALS = credentials('41b7759f-dc7c-41cf-a965-1880286f75fb') 
        DOCKER_IMAGE_NAME = 'shivaavvari/flaskapp' // e.g., 'myuser/my-app'
        DOCKER_IMAGE_TAG = "${env.BUILD_NUMBER}" // Or use a specific version, e.g., '1.0.0'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git 'https://github.com/shivaavvari/sample_app.git' // Replace with your Git repository URL
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG} ."
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub using stored credentials
                    sh "echo ${DOCKERHUB_CREDENTIALS_PSW} | docker login -u ${DOCKERHUB_CREDENTIALS_USR} --password-stdin"
                    
                    // Push the Docker image
                    sh "docker push ${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}"
                    
                    // Logout from Docker Hub (optional, but good practice)
                    sh "docker logout"
                }
            }
        }
    }
}
