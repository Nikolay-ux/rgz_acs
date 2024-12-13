pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/Nikolay-ux/rgz_acs.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t your-dockerhub-username/your-app:latest .'
            }
        }
        stage('Push to DockerHub') {
            steps {
                withDockerRegistry([credentialsId: 'dockerhub-credentials-id']) {
                    sh 'docker push your-dockerhub-username/your-app:latest'
                }
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop your-app || true
                docker rm your-app || true
                docker run -d --name your-app -p 80:80 your-dockerhub-username/your-app:latest
                '''
            }
        }
    }
}

