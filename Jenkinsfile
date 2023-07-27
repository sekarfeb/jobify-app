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

        stage('Build') {
            steps {
                // Build your MERN app (if needed)
                sh 'cd backend && npm run build'
            }
        }
        
        
        
        
        
    }
}