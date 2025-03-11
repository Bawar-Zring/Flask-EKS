# Flask App with AWS EKS, PostgreSQL, and Redis
This project deploys a Flask application on an AWS EKS (Elastic Kubernetes Service) cluster. The application interacts with a PostgreSQL database and a Redis cache, both deployed using AWS services.

## Architecture
- AWS EKS: Kubernetes cluster running the Flask application.
- Amazon RDS (PostgreSQL): Database for storing application data.
- Amazon ElastiCache (Redis): Caching layer for performance optimization.
- Terraform: Infrastructure as Code (IaC) to provision AWS resources.
- Kubernetes (K8s): Manages the Flask application's deployment and services.

## Prerequisites
- Terraform installed
- AWS CLI configured
- kubectl installed
- Docker installed
- A valid AWS account

## Deployment Steps
1. Clone the Repository
   ```
     git clone <repository_url>
     cd <repository_name>
   ```
2. Build and Push the Docker Image in Case my image not available anymore in Dockerhub (Optional)
   ```
    docker build -t <your_dockerhub_username>/my-flask-app:v1 .
    docker push <your_dockerhub_username>/my-flask-app:v1
   ```
3. Provision AWS Infrastructure with Terraform
   ```
    terraform init
    terraform apply --auto-approve
   ```
4. Configure kubectl
   ```
    aws eks  update-kubeconfig --region us-east-1 --name eks-cluster
   ```
5. Deploy the Application to Kubernetes
   ```
     kubectl apply -f K8s/
   ```
6. Check Application Status
   ```
    kubectl get pods
    kubectl get svc 
   ```
7. Test the Application
   Retrieve the EXTERNAL-IP of the flask-service and visit:
   ```
    http://<EXTERNAL-IP>:5000/health
   ```
# Environment Variables
The application uses environment variables for database and Redis configuration:
   ```
    POSTGRES_USER: admin_test
    POSTGRES_PASSWORD: Admin1234
    POSTGRES_DB: testdb
    POSTGRES_HOST: <retrieved from AWS endpoints>
    POSTGRES_PORT: 5432
    REDIS_HOST: <retrieved from AWS endpoints>
    REDIS_PORT: 6379
   ```

# Cleanup
```
terraform destroy --auto-approve
```



