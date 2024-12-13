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
                sh 'docker build -t myusername/your-app:latest .'
            }
        }
        stage('Deploy Container') {
            steps {
                sh '''
                docker stop your-app || true
                docker rm your-app || true
                docker run -d --name your-app -p 80:80 myusername/your-app:latest
                '''
            }
        }
    }
}

