pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Docker Build') {
    	agent any
            steps {
      	        sh 'cd backend && docker build -t sekarfeb/jenkins-jobify-backend:latest .'
            }
        }
        
        
        
        
        
    }
}