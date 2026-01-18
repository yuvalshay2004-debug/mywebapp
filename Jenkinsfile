pipeline {
    agent any

    environment {
        // כאן ID של ה-Credential ב-Jenkins שמכיל username + password או token של Docker Hub
        DOCKER_CREDENTIALS_ID = 'dockerhub-creds'
        DOCKER_IMAGE = "yuvalzoro6767/mywebapp:latest"
        KUBE_DEPLOYMENT_YAML = "k8s/mywebapp-deployment.yaml"
        KUBE_SERVICE_YAML = "k8s/mywebapp-service.yaml"
    }

    stages {

        stage('Build Docker Image') {
            steps {
                script {
                    sh "docker build -t $DOCKER_IMAGE ."
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    // גישה ל-Credentials ושימוש ב-shell login
                    withCredentials([usernamePassword(credentialsId: "$DOCKER_CREDENTIALS_ID", usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                        sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                        sh "docker push $DOCKER_IMAGE"
                        sh 'docker logout'
                    }
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    sh "kubectl apply -f $KUBE_DEPLOYMENT_YAML"
                    sh "kubectl apply -f $KUBE_SERVICE_YAML"
                }
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline finished successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Check the logs above.'
        }
    }
}

