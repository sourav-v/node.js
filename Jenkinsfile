pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/sourav-v/node.js.git'          }
        }

        stage('Build Docker Image') {
            steps {
                script {
                   sh "docker build -t nodejs ."
                }
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                    docker stop nodejs-app || true
                    docker rm nodejs-app || true
                    docker run -d --name nodejs-app -p 3005:3005 nodejs
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
}
