pipeline {
    agent any 
    
    stages { 
        stage('SCM Checkout') {
            steps {
                retry(3) {
                    git branch: 'main', url: 'https://github.com/ChanukaWelagedara/Dev_Opps'
                }
            }
        }
        stage('Build Docker Image') {
            steps {  
                bat 'docker build -t chanukawelagedara/nodeapp-cuban:%BUILD_NUMBER% .'
            }
        }
        stage('Login to Docker Hub') {
            steps {
                withCredentials([string(credentialsId: 'myapp-password', variable: 'myapp-dockerhubpass')]) {
                    script {
                        bat "docker login -u chanukawelagedara -p %myapp-password%"
                    }
    
}
                
            }
        }
        stage('Push Image') {
            steps {
                bat 'docker push chanukawelagedara/nodeapp-cuban:%BUILD_NUMBER%'
            }
        }
    }
    post {
        always {
            bat 'docker logout'
        }
    }
}
