
pipeline {
    agent any

    stages {
        stage('Checkout GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/arulovia2006/kubernets.git'
            }
        }

        stage('Verify Kubernetes') {
            steps {
                bat 'kubectl get nodes'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                bat 'kubectl apply -f "manifests\\web-configmap.yaml"'
                bat 'kubectl apply -f "manifests\\web-deployment.yaml"'
                bat 'kubectl apply -f "manifests\\web-service.yaml"'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'kubectl rollout status deployment/devops-web -n devops-lab --timeout=180s'
                bat 'kubectl get pods -n devops-lab'
                bat 'kubectl get services -n devops-lab'
            }
        }
    }
}
