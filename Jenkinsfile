pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh 'docker build . -t mywebapp'
            }
        }

        stage('Test') {
            steps {
                echo 'Hello Jenkins!'
            }
        }

        stage('Deploy') {
            steps {
                // stop and remove the container if no longer exists
                sh 'docker stop mywebapp || true'
                sh 'docker rm mywebapp || true'

                // new run with name
                sh 'docker run -d --name mywebapp -p 5000:5000 mywebapp'
            }
        }
    }
}



