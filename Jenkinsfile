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
                bat 'docker build -t dev1:%BUILD_NUMBER% .'
            }
        }

        stage('Load Image into Minikube') {
            steps {
                bat 'minikube image load dev1:%BUILD_NUMBER%'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
            }
        }

        stage('Update Kubernetes Image') {
            steps {
                bat 'kubectl set image deployment/devops-web-deployment devops-container=dev1:%BUILD_NUMBER%'
            }
        }

        stage('Check Deployment') {
            steps {
                bat 'kubectl rollout status deployment/devops-web-deployment'
            }
        }

    }
}