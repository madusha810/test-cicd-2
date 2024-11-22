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
                script {
                    sh 'docker build -t nodeapp-cuban:latest .'
                }
            }
        }
        // stage('Push Docker Image') {
        //     steps {
        //         script {
        //             docker.withRegistry('https://index.docker.io/v1/', 'dockerhub') {
        //                 sh 'docker push madusha810/nodeapp-cuban:latest'
        //             }
        //         }
        //     }
        // }

        stage('Run Docker Container') {
            steps {
                script {
                    sh "docker run --name node-app-container nodeapp-cuban"
                }
            }
        }


    }
    
    post {
        always {
            sh 'docker logout || true' // Ensures logout doesn't fail the pipeline if already logged out
        }
    }
}
