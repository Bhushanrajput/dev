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
                bat 'docker build -t dev1 .'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat 'docker stop dev-container1 || exit 0'
            }
        }

        stage('Remove Old Container') {
            steps {
                bat 'docker rm dev-container1 || exit 0'
            }
        }

        stage('Run New Container') {
            steps {
                bat 'docker run -d -p 8082:80 --name dev-container1 dev1'
            }
        }

    }
}