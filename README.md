# Coworking Analytics Application

This project demonstrates a complete containerized deployment workflow for a Python analytics service using Docker, AWS, and Kubernetes.  
The application is packaged as a Docker image and stored in Amazon ECR, with automated builds handled by AWS CodeBuild.  
Each code change triggers CodeBuild to build a new Docker image, tag it using semantic versioning, and push it to ECR.  

The application is deployed on an Amazon EKS cluster using Kubernetes Deployments and Services.  
Kubernetes ConfigMaps are used to store non-sensitive configuration such as database host, port, and username.  
Sensitive data like database passwords are stored securely using Kubernetes Secrets.  

The service is exposed externally via a Kubernetes LoadBalancer, allowing access to health and readiness endpoints.  
Liveness and readiness probes ensure that Kubernetes can monitor application health and restart containers when needed.  
A PostgreSQL database is deployed inside the cluster and accessed by the application through an internal Kubernetes Service.  

Application logs and runtime metrics are collected using Amazon CloudWatch Container Insights.  
This allows monitoring pod health, resource usage, and application logs directly from the AWS Console.  

To deploy a new version, push changes to the repository, let CodeBuild generate a new image version, and update the Kubernetes Deployment image tag.  

## Stand-Out Considerations
The deployment can be improved by specifying CPU and memory requests and limits to ensure predictable scheduling.  
A small instance type such as t3.small is sufficient for this workload due to low compute and memory requirements.  
Infrastructure costs can be reduced by using a single-node cluster for development and scaling resources only when needed.
