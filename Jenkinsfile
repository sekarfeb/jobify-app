pipeline {
    agent any

   environment { 

        registry = "sekarfeb/jobify-app" 

        registryCredential = 'sekardocker' 

        dockerImage = '' 

    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Docker Build0') {
    	        steps {
                    script{
                        dockerImage = docker.build registry + ":latest"
                    }
      	        
            }
        }
        


        stage('Docker Build') {
    	agent any
            steps {
      	        sh 'cd backend && docker build -t sekarfeb/jenkins-jobify-backend:latest .'
            }
        }
        
        stage('Login to Docker Hub') {      	
            steps{                       	
	            sh 'echo $DOCKERHUB_CREDENTIALS_PSW | sudo docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                		
	            echo 'Login Completed'      
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