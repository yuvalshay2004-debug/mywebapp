pipeline {
    agent any
    environment {
	DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
        DOCKER_IMAGE = "yuvalzoro6767/mywebapp:latest"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t $DOCKER_IMAGE .'
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh 'kubectl apply -f mywebapp-deployment.yaml'
                    sh 'kubectl apply -f mywebapp-service.yaml'
                }
            }
        }
    }
}

