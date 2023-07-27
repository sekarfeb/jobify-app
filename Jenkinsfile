pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
    	agent any
            steps {
      	        sh 'cd backend && docker build -t sekarfeb/jenkins-jobify-backend:latest .'
            }
        }

        stage('Push Docker Image') {
            steps {
                // Use 'sh' step to run shell commands with password input from stdin
                withCredentials([usernamePassword(credentialsId: 'sekardocker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                }
                sh "docker push sekarfeb/jenkins-jobify-backend:latest"
            }
        }        
        
    }
}