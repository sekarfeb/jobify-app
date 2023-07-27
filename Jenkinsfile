pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'cd backend && npm install'
            }
        }

        stage('Docker Build') {
    	agent any
            steps {
                sh 'cd backend'
      	        sh 'docker build -t shanem/spring-petclinic:latest .'
            }
        }
        
        
        
        
        
    }
}