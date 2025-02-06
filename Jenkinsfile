pipeline {
    agent any


    stages {
        stage("Checkout") {
            steps {
                git branch: 'main', url: 'https://github.com/ridodomayana/netflix-cd.git'
            }
        }
        stage("Validating YAML Files") {
            steps {
                echo 'Validating Kubernetes YAML files...'
                sh 'kubectl apply --dry-run=client -f deployment.yml'
                sh 'kubectl apply --dry-run=client -f service.yml'
            }
        }
        stage("Apply YAML Files") {
            steps {
                echo 'Applying Kubernetes YAML files...'
                sh '''
                kubectl apply -f deployment.yml
                kubectl apply -f service.yml
                '''
            }
        }
    }
    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed. Please check logs.'
        }
    }
}
