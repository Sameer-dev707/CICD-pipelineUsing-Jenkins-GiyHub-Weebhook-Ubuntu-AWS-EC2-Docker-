pipeline {
    agent any

    environment {
        CONTAINER_NAME = "nestjs-app"
        IMAGE_NAME = "nestjs-image"
        EMAIL = "msameerhassan11@gmail.com"
        PORT = "3000"
    } 

    stages {
        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME} ."
            }
        } 

        stage('Stop & Remove Previous Container') {
            steps {
                sh '''
                    docker stop ${CONTAINER_NAME} || true 
                    docker rm ${CONTAINER_NAME} || true 
                '''
            }
        } 

        stage('Run Docker Container') {
            steps {
                sh "docker run -d -p ${PORT}:${PORT} --name ${CONTAINER_NAME} ${IMAGE_NAME}"
            }
        } 

        stage('Send Email Notification') {
            steps {
                emailext (
                    subject: "NestJS App Deployed Successfully on EC2",
                    body: "Your NestJS app is deployed and running on port ${PORT}!",
                    to: "${EMAIL}"
                )
            }
        } 
    }
}