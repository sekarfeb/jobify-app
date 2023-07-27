pipeline {
    agent any

    environment {     
    DOCKERHUB_CREDENTIALS= credentials('sekardocker')     
    }
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
        

        stage('Push Docker Image') {
            steps {
                // Use 'sh' step to run shell commands
                sh "docker login -u YOUR_DOCKERHUB_USERNAME -p YOUR_DOCKERHUB_PASSWORD"
                sh "docker push sekarfeb/jenkins-jobify-backend:latest"
            }
        }
        
        
        
        
    }
}