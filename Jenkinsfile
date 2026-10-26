pipeline {
    agent any

    environment {
        KUBECONFIG = 'C:\\ProgramData\\Jenkins\\.kube\\config'
        IMAGE_NAME = 'prathyushajanga07/container-app:v1'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/prathyushajanga07-tech/kubernetes-jenkins-exp9.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t %IMAGE_NAME% .'
            }
        }

        stage('Push Docker Image') {
            steps {
                bat 'docker push %IMAGE_NAME%'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f deployment.yaml'
                bat 'kubectl apply -f service.yaml'
                bat 'kubectl rollout status deployment/container-app --timeout=120s'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl get pods'
                bat 'kubectl get services'
            }
        }
    }
}
