pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = credentials('dockerhub-username') ?: 'sarwar1512'
        DOCKERHUB_PASSWORD = credentials('dockerhub-password') ?: 'sarwar@1#'
        DOCKER_IMAGE_NAME = "sarwar1512/simplespringboot:0.0.1-SNAPSHOT"
    }
    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: 'master']], userRemoteConfigs: [[url: 'https://github.com/sarwar-max/greetingSpringBoot.git']]])
            }
        }
        stage('Build and Test') {
            steps {
                // Build the Spring Boot application using Maven
                sh 'mvn clean install'
            }
        }
        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile
                sh "docker build -t ${DOCKER_IMAGE_NAME} ."
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub
                sh "docker login -u ${DOCKERHUB_USERNAME} -p ${DOCKERHUB_PASSWORD}"
                
                // Push the Docker image to Docker Hub
                sh "docker push ${DOCKER_IMAGE_NAME}"
            }
        }
    }
    post {
        always {
            // Clean up any Docker images and containers
            sh "docker rmi ${DOCKER_IMAGE_NAME}"
        }
    }
}
