
## 🔄 Deployment Workflow

1. **Provision Infrastructure with Terraform Cloud**  
   - Create a **Terraform Cloud workspace** and connect your GitHub repository.  
   - Set **AWS credentials** in Terraform Cloud workspace variables:  
     ```
     AWS_ACCESS_KEY_ID
     AWS_SECRET_ACCESS_KEY
     AWS_REGION
     ```
   - Terraform Cloud provisions: VPC, subnets, security groups, ECS cluster & service, and networking resources.

2. **Build and Push Docker Image**  
   - Build Docker image:
     ```bash
     docker build -t my-app -f ./app/dockerfile ./app
     ```
   - Push the image to Amazon ECR:
     ```bash
     aws ecr get-login-password --region <AWS_REGION> \
     | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com

     docker tag my-app:latest <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/my-app:latest
     docker push <AWS_ACCOUNT_ID>.dkr.ecr.<AWS_REGION>.amazonaws.com/my-app:latest
     ```

3. **Deploy Docker Image to ECS**  
   - Update ECS service to deploy the new image:
     ```bash
     aws ecs update-service --cluster my-cluster --service my-service --force-new-deployment
     ```
   - ECS Fargate launches tasks using the updated Docker image.

4. **Access the Application**  
   - ECS tasks run in a **public subnet** with public IPs.  
   - Open the app in your browser:
     ```
     http://<public-ip>
     ```
   - Optional: Add an **Application Load Balancer (ALB)** for a stable URL.

### CI/CD
- **GitHub Actions** automatically builds Docker images and deploys updates to ECS on each commit to `main`.  
- Terraform Cloud ensures reproducible infrastructure provisioning.

## 📌 Next Steps

- Enable **Auto Scaling** for ECS tasks.  
- Integrate **CloudFront CDN** for global delivery.  
- Configure **CloudWatch** monitoring and alarms.  
- Implement **least-privilege IAM roles** for secure access.

## 💡 References

- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)  
- [Docker Documentation](https://docs.docker.com/)  
- [AWS ECS Documentation](https://docs.aws.amazon.com/ecs/latest/userguide/what-is-ecs.html)  
- [Terraform Cloud](https://www.terraform.io/cloud)

# aws-web-app
