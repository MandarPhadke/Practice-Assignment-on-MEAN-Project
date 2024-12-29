pipeline {
    agent any

    stages {
        stage('Build Frontend Image') {
            steps {
                sh 'docker build -t resumeai-frontend ./ResumeBuilderAngular'
            }
        }
        stage('Build Backend Image') {
            steps {
                sh 'docker build -t resumeai-backend ./ResumeBuilderBackend'
            }
        }
        stage('Push to ECR') {
            steps {
                sh '''
                aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 975050024946.dkr.ecr.us-west-2.amazonaws.com
                docker tag resumeai-frontend:latest 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-frontend:latest
                docker tag resumeai-backend:latest 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-backend:latest
                docker push 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-frontend:latest
                docker push 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-backend:latest
                '''
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                sh '''
                kubectl apply -f k8s/frontend-deployment.yaml
                kubectl apply -f k8s/backend-deployment.yaml
                kubectl apply -f k8s/frontend-service.yaml
                kubectl apply -f k8s/backend-service.yaml
                '''
            }
        }
    }
}
