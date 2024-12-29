# Practice-Assignment-on-MEAN-Project
Practice Assignment on MEAN Project

commands to 
build docker images

docker build -t resumeai-frontend ./ResumeBuilderAngular
docker build -t resumeai-backend ./ResumeBuilderBackend

push it to ECR

aws ecr get-login-password --region us-west-2 | docker login --username AWS --password-stdin 975050024946.dkr.ecr.us-west-2.amazonaws.com
docker tag resumeai-frontend:latest 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-frontend:latest
docker tag resumeai-backend:latest 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-backend:latest
docker push 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-frontend:latest
docker push 975050024946.dkr.ecr.us-west-2.amazonaws.com/resumeai-backend:latest

creating a Kubernetes cluster and deploy the application using EKS
kubectl apply -f k8s/frontend-deployment.yaml
kubectl apply -f k8s/backend-deployment.yaml
kubectl apply -f k8s/frontend-service.yaml
kubectl apply -f k8s/backend-service.yaml
