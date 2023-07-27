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

        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("my-docker-image:latest", "./backend")
                }
            }
        }
        
        
        
        
        
    }
}