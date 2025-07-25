# Serverless CI/CD

This project provides a serverless CI/CD pipeline using AWS CloudFormation and Docker. It is designed to automate the deployment of applications in a scalable and efficient manner.
This demo is using the following AWS components:
- **VPC, Subnets, and Networking:**
  - Creates a dedicated VPC with two public subnets, an Internet Gateway, and route tables for public access.
- **Security Groups:**
  - Security groups for the Network Load Balancer (NLB) and ECS Fargate service.
- **Amazon ECR:**
  - Container image repository for storing Docker images.
- **Amazon ECS (Fargate):**
  - ECS Cluster, Task Definition, and Fargate Service to run your application in containers.
  - Log group for ECS task logs.
- **Elastic Load Balancing (NLB):**
  - Network Load Balancer, Target Group, and Listener to distribute traffic to ECS tasks.
- **Amazon API Gateway:**
  - REST API that routes requests to the ECS service via the NLB, and a separate endpoint for a Lambda function.
- **AWS Lambda:**
  - Example Lambda function with execution role, integrated with API Gateway.
- **AWS CodeBuild:**
  - Two CodeBuild projects: one for building and pushing Docker images, and one for scaling up the ECS service after deployment.
- **AWS CodePipeline:**
  - Complete CI/CD pipeline integrating GitHub (source), CodeBuild (build), ECS (deploy), and CodeBuild (scale up).
- **Amazon S3:**
  - S3 bucket for storing pipeline artifacts.
- **IAM Roles:**
  - Roles and policies for ECS tasks, Lambda, CodeBuild, and CodePipeline.

This setup enables automated builds and deployments from GitHub to a scalable, serverless container environment, with API endpoints exposed via API Gateway and Lambda integration.


## Project Structure

- `app.py` - Main application code.
- `buildspec.yaml` - Build specification for CI/CD pipeline (e.g., AWS CodeBuild).
- `cloudformation/infrastructure.yaml` - AWS CloudFormation template for infrastructure provisioning.
- `Dockerfile` - Docker image definition for the application.
- `imagedefinitions.json` - (Optional) Image definitions for deployment.

## Prerequisites

- Python 3.7+
- Docker
- AWS CLI configured with appropriate permissions

## Setup & Deployment

1. **Deploy Infrastructure:**
   ```bash
   aws cloudformation deploy \
     --template-file cloudformation/infrastructure.yaml \
     --stack-name your-stack-name \
     --capabilities CAPABILITY_NAMED_IAM
   ```

2. Change app.py and commit to the git repo you specified during Cloudformation execution. Pipeline will run and the CD will be done

## Customization

- Modify `app.py` to update application logic.
- Update `cloudformation/infrastructure.yaml` to change infrastructure resources.
- Edit `Dockerfile` to adjust the container build process.

## CloudFormation Infrastructure

The `cloudformation/infrastructure.yaml` template provisions a complete CI/CD pipeline and application hosting environment using the following AWS components:

## License

This project is provided as-is. Please update with your own license as needed. 