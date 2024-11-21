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
                sh 'docker build -t madusha810/nodeapp-cuban:1 .'
            }
        }
        stage('Push') {
            steps {
                     docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                     sh 'docker push madusha810/nodeapp-cuban:1'
                 }
              }
        
            }
        }
        // stage('Push Image') {
        //     steps {
        //         sh 'docker push madusha810/nodeapp-cuban:1'
        //     }
        // }
    }
    // post {
    //     always {
    //         sh 'docker logout'
    //     }
    // }
