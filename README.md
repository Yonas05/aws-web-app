# 🌐 AWS Web Application

This repository demonstrates deploying a scalable web application on AWS using **Terraform** and **Ansible** or **Docker**.

## 📦 Project Structure


## 🔄 Deployment Workflow

### Option 1: EC2 + Ansible
1. Use **Terraform** to create EC2 instances and security groups.
2. Use **Ansible** to install web server and deploy application code.

### Option 2: ECS / Docker
1. Build **Docker image** of your app.
2. Push image to **ECR**.
3. Terraform provisions ECS cluster and deploys the Docker container.

### CI/CD
- Connect **GitHub** repo to **Terraform Cloud** for automated infrastructure provisioning.
- Use **GitHub Actions** to build Docker images and deploy updates.

## 📌 Next Steps

- Add **Auto Scaling Groups** for EC2/ECS.
- Integrate **CloudFront CDN** for global delivery.
- Configure **CloudWatch** monitoring.
- Add **IAM roles** for secure permissions.

## 💡 References

- [Terraform AWS Provider](https://registry.terraform.io/providers/hashicorp/aws/latest/docs)
- [Ansible Documentation](https://docs.ansible.com/)
- [AWS ECS Documentation](https://docs.aws.amazon.com/ecs/latest/userguide/what-is-ecs.html)
