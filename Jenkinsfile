pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "coinbase-service:${env.BUILD_ID}"
        REGISTRY = "your-docker-registry"
    }
    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Deploy to Development') {
            steps {
                sh 'kubectl apply -f deployment.yaml --record'
            }
        }
        stage('Testing') {
            steps {
                sh 'kubectl rollout status deployment/coinbase-service'
              
            }
        }
        stage('Deploy to Production') {
            steps {
                sh 'kubectl apply -f blue-green.yaml --record'
            }
        }
    }
}
