pipeline {
    agent any
    
    environment {
        // Define environment variables if needed
        DOCKER_IMAGE_NAME = "spring-boot-docker"
        SPRING_PROFILE = "default"
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from your Git repository
                git branch: 'main', url: 'https://github.com/sarwar-max/greetingSpringBoot.git'
            }
        }
        
        stage('Build Spring Boot Application') {
            steps {
                bat 'mvn clean package' // Use "bat" for Windows batch commands
            }
        }
        
        stage('Build Docker Image') {
            steps {
                bat 'docker build -t ${DOCKER_IMAGE_NAME}:${BUILD_NUMBER} .' // Use "bat" for Windows batch commands
            }
        }
        
        stage('Push Docker Image') {
            steps {
                bat 'docker push ${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}' // Use "bat" for Windows batch commands
            }
        }
        
        stage('Deploy to Docker') {
            steps {
                bat "docker run -d --name ${DOCKER_IMAGE_NAME} -e SPRING_PROFILES_ACTIVE=${SPRING_PROFILE} -p 8080:8080 ${DOCKER_IMAGE_NAME}:${BUILD_NUMBER}" // Use "bat" for Windows batch commands
            }
        }
    }
    
    
}
