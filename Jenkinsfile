pipeline {
    agent any
    stages {
        stage('Deploy on k8s') {
            steps {
                withCredentials([ string(credentialsId: 'minikube-credentials', variable: 'api_token') ]) {
                    sh 'kubectl --token $api_token --server https://host.docker.internal:63468  --insecure-skip-tls-verify=true apply -f ./k8s/deployment.yaml '
                    sh 'kubectl --token $api_token --server https://host.docker.internal:63468  --insecure-skip-tls-verify=true apply -f ./k8s/service.yaml '
                }
            }
        }
    }
    post {
        success {
            echo 'Redis deployed.'
        }
        failure {
            echo 'Failed to deploy Redis.'
        }
    }
}
