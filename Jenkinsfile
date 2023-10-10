pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Checkout and Build') {
            steps {
                script {
                    // Checkout the 'master' branch from your Git repository
                    checkout([$class: 'GitSCM',
                        branches: [[name: '*/master']],
                        userRemoteConfigs: [[url: 'https://github.com/sarwar-max/greetingSpringBoot']]])

                    // Build your Maven project
                    bat 'mvn clean install'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    // Build a Docker image from your Spring Boot application
                    bat "docker build -t sarwar1512/spring-boot-docker ."
                }
            }
        }

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    bat 'docker login -u sarwar1512 -p sarwar@1#'

                    // Push the Docker image to Docker Hub
                    bat "docker push sarwar1512/spring-boot-docker"
                }
            }
        }
    }
}
