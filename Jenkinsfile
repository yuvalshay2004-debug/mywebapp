pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "yuvalzoro6767/mywebapp:latest"
        KUBECONFIG = "/Users/yuahi/.kube/config" // צריך להצביע ל-kubeconfig של Mac
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
                    sh 'kubectl apply -f deployment.yaml'
                    sh 'kubectl apply -f service.yaml'
                }
            }
        }
    }
}

