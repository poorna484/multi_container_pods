pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig')
    }

    stages {

        stage('Checkout Code') {
            steps {
                // Pull the repo that contains pod YAML
                checkout scm
            }
        }

        stage('Deploy Multi-Container Pod') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl apply -f pod-multi.yaml
                '''
            }
        }

        stage('Verify Pod') {
            steps {
                sh '''
                export KUBECONFIG=$KUBECONFIG
                kubectl get pods -o wide
                kubectl describe pod multi-container-pod
                '''
            }
        }
    }
}
