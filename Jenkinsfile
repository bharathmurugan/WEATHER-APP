pipeline {
    agent any

    environment {
        IMAGE_NAME = 'bharathmurugan/WEATHER-APP'
        CONTAINER_NAME = 'WEATHER-APP-container'
        KUBE_DEPLOYMENT = 'WEATHER-APP-deployment'
        KUBE_NAMESPACE = 'default'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/bharathmurugan/WEATHER-APP'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $IMAGE_NAME'
                }
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s-deployment.yaml'
            }
        }
    }
}