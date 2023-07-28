pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image - Backend') {
    	agent any
            steps {
      	        sh 'cd backend && docker build -t sekarfeb/jenkins-jobify-backend:latest .'
            }
        }

        stage('Push Docker Image - Backend') {
            steps {
                // Use 'sh' step to run shell commands with password input from stdin
                withCredentials([usernamePassword(credentialsId: 'sekardocker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                }
                sh "docker push sekarfeb/jenkins-jobify-backend:latest"
            }
        }

        stage('Deploy to GKE - Backend') {
            steps {
                // Authenticate with GKE using service account key
                withCredentials([file(credentialsId: 'gke-service-account-key', variable: 'SERVICE_ACCOUNT_KEY')]) {
                    sh "gcloud auth activate-service-account --key-file=${SERVICE_ACCOUNT_KEY}"
                }
                
                // Set the GKE context
                sh "gcloud container clusters get-credentials cluster-1 --region=us-central1-c --project=amazing-thought-387010"

                // Apply the Kubernetes Deployment
                sh "kubectl get namespace"
                sh "cd backend && kubectl apply -f deployment.yaml"
            }
        }        
        
        stage('Build Docker Image - Frontend') {
    	agent any
            steps {
      	        sh 'cd backend && docker build -t sekarfeb/jenkins-jobify-frontend:latest .'
            }
        }

        stage('Push Docker Image - Frontend') {
            steps {
                // Use 'sh' step to run shell commands with password input from stdin
                withCredentials([usernamePassword(credentialsId: 'sekardocker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                }
                sh "docker push sekarfeb/jenkins-jobify-frontend:latest"
            }
        }

        stage('Deploy to GKE - Frontend') {
            steps {
                // Authenticate with GKE using service account key
                //withCredentials([file(credentialsId: 'gke-service-account-key', variable: 'SERVICE_ACCOUNT_KEY')]) {
                //    sh "gcloud auth activate-service-account --key-file=${SERVICE_ACCOUNT_KEY}"
                //}
                
                // Set the GKE context
                //sh "gcloud container clusters get-credentials cluster-1 --region=us-central1-c --project=amazing-thought-387010"

                // Apply the Kubernetes Deployment
                sh "cd backend && kubectl apply -f deployment.yaml"
            }
        }        
    }
}