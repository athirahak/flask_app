pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/athirahak/flask_app.git'
            }
        }
        stage('Build') {
            steps {
                script {
                    dockerImage = docker.build("myapp:latest")
                }
            }
        }
        stage('Test') {
            steps {
                script {
                    dockerImage.inside {
                        sh 'python -m unittest discover'
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
                        dockerImage.push('myapp:latest')
                    }
                }
            }
        }
    }
}
