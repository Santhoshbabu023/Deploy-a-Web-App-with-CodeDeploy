# Deploy a Web App with CodeDeploy

## Introduction
In this project, I demonstrated deploying a web app using AWS CloudFormation, automation scripts, and CodeDeploy. This project helped me learn about automated deployments, infrastructure as code (IaC), and how to safely roll back deployments during failures.

## Key Tools and Concepts

### Services Used:
- **AWS CloudFormation**: For defining infrastructure as code.
- **EC2**: For hosting the web app.
- **VPC**: To manage networking securely.
- **Subnet**: To organize EC2 instances.
- **Internet Gateway (IGW)**: For internet access.
- **Route Table**: For routing traffic between instances and the internet.
- **Security Group**: For controlling inbound/outbound traffic.
- **IAM**: For managing permissions and roles.
- **SSM**: For dynamically referencing the latest Amazon Linux AMI.

### Key Concepts Learned:
- Infrastructure as Code (IaC) for consistent and reproducible deployments.
- Setting up public subnets, routing, and managing secure access using security groups.
- Using AWS Systems Manager (SSM) to dynamically retrieve the latest Amazon Linux AMI.
- Assigning EC2 instance roles for security and permissions management.

## Project Reflection

- **Time Taken**: 1 day.
- **Most Challenging Part**: Configuring VPC networking and routing correctly for internet access.
- **Most Rewarding**: Successfully launching the EC2 instance with secure HTTP access.

This project is part five of a series of DevOps projects where I’m building a CI/CD pipeline. I'll work on the next project soon, focusing on automating deployments with Jenkins or AWS CodePipeline for continuous integration and delivery.

## Deployment Environment
For CodeDeploy, I launched an EC2 instance and a VPC:
- **EC2 Instance**: Deployment target for the web app.
- **VPC**: Provides secure networking and access control.

I used **AWS CloudFormation** to automate the creation of these resources, making it easier to manage and delete them when necessary.

Other resources created in this template include:
- **Security Group**: To manage inbound and outbound access to EC2.
- **IAM Role & Instance Profile**: To grant permissions for CodeDeploy.
- **Key Pair**: For SSH access to the EC2 instance.

## Deployment Scripts

I wrote several scripts to automate tasks during deployment:

1. **install_dependencies.sh**: Installs required packages like Tomcat and Apache HTTP Server.
2. **start_server.sh**: Starts Tomcat and Apache services.
3. **stop_server.sh**: Stops Tomcat and Apache services before updates.

## appspec.yml & buildspec.yml

### **appspec.yml**:
Defines the deployment lifecycle with hooks to install dependencies and manage server states.

### **buildspec.yml**:
Configures the build process to package deployment artifacts (e.g., the WAR file) and prepare them for deployment.

## Setting Up CodeDeploy

1. **CodeDeploy Application**: Represents the web app being deployed.
2. **Deployment Group**: Specifies EC2 instances and deployment settings.
3. **IAM Role for CodeDeploy**: Grants CodeDeploy permission to access EC2 instances and manage deployments.
4. **Tags**: Used to target specific EC2 instances. I used the `CodeDeployEC2` tag to identify the instances for deployment.

## Deployment Configurations

I selected **CodeDeployDefault.AllAtOnce** for deployment, which deploys all target instances simultaneously. This configuration is faster but has a higher risk of failure.

The **CodeDeploy Agent** installed on EC2 instances listens for deployment commands and executes the deployment process as defined in the appspec.yml file.

## Success!

Once the deployment was complete, I verified it by visiting the web application URL. The updated version of the application was live, confirming that the deployment was successful and changes were applied correctly.

## Key Learnings

- **Launch Deployment Architecture using CloudFormation**.
- **Prepare Deployment Scripts and appspec.yml for CodeDeploy**.
- **Set up CodeDeploy Applications and Deployment Groups**.
- **Deploy a Web Application using CodeDeploy**.
- **Implement Disaster Recovery and Roll Back a Deployment**.
