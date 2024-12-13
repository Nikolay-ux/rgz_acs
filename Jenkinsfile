pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t your-dockerhub-username/your-app:latest .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([url: 'https://index.docker.io/v1/', credentialsId: 'dockerhub-credentials-id']) {
                    sh 'docker push your-dockerhub-username/your-app:latest'
                }
            }
        }
    }
}

