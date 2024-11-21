pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/madusha810/test-cicd-2'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                sh 'docker build -t madusha810/nodeapp-cuban:1'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'dh-password-id', variable: 'dockerhub-password')]) {
                    script {
                        sh "docker login -u madusha810 -p %dockerhub-password%"
                    }
                }
            }
        }
        stage('Push Image') {
            steps {
                sh 'docker push madusha810/nodeapp-cuban:1'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}