pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "your-dockerhub-username/your-app:latest"
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Nikolay-ux/rgz_acs.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Push to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy Container') {
            steps {
                script {
                    sh 'docker stop app || true && docker rm app || true'
                    sh 'docker run -d --name app -p 5000:5000 $DOCKER_IMAGE'
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

