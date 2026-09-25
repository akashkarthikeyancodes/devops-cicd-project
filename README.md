# Automated CI/CD Pipeline with Jenkins, Docker & AWS

## 📌 Project Overview

This project demonstrates a CI/CD workflow for a containerized web application using GitHub, Jenkins, Docker, and AWS.

Whenever code is pushed to the GitHub repository, a GitHub Webhook automatically triggers Jenkins. Jenkins checks out the latest source code, builds the Docker image, authenticates with Amazon ECR, and pushes the image to the ECR repository.

The Docker image is then deployed and run on an AWS EC2 instance.

---

## 🏗️ Architecture

![Project Architecture](./architecture.png)

## 🛠️ Technologies Used

- Git
- GitHub
- GitHub Webhooks
- Jenkins
- Jenkins Pipeline
- Docker
- Amazon EC2
- Amazon ECR
- AWS IAM
- Linux
- Nginx

---

## 🚀 CI/CD Workflow

### 1. Source Code Management

The application source code is maintained in GitHub.

Repository:

https://github.com/akashkarthikeyancodes/devops-cicd-project

Project structure:

    devops-cicd-project/
    │
    ├── Dockerfile
    ├── Jenkinsfile
    └── index.html

---

### 2. GitHub Webhook

A GitHub Webhook is configured to notify Jenkins whenever code is pushed to the repository.

Webhook endpoint:

    http://<JENKINS-EC2-IP>:8080/github-webhook/

The webhook was successfully tested with an HTTP 200 response.

A real GitHub push also successfully triggered Jenkins automatically.

---

### 3. Jenkins Pipeline

Jenkins is configured using a Jenkins Pipeline defined in the `Jenkinsfile`.

Pipeline stages:

    Checkout
        ↓
    Build Docker Image
        ↓
    Authenticate with Amazon ECR
        ↓
    Tag Docker Image
        ↓
    Push Image to Amazon ECR

---

### 4. Docker

The application is packaged into a Docker image using Nginx Alpine.

The Dockerfile copies the HTML application into the Nginx web server directory.

    FROM nginx:alpine

    COPY index.html /usr/share/nginx/html/index.html

Docker provides a consistent environment for running the application.

---

### 5. Amazon ECR

The Docker image is stored in Amazon Elastic Container Registry (ECR).

ECR Repository:

    devops-cicd-app

AWS Region:

    ap-south-1

Image Tag:

    latest

---

### 6. AWS EC2

The Docker container is deployed and run on an Amazon EC2 instance.

The application is exposed through port 80.

Example deployment commands:

    docker pull <ECR-IMAGE>

    docker stop devops-cicd-app

    docker rm devops-cicd-app

    docker run -d -p 80:80 --name devops-cicd-app <ECR-IMAGE>

The application was successfully verified through the EC2 public IP.

---

## 🔄 CI/CD Flow

A developer makes a change to the application.

For example:

    index.html

The developer commits and pushes the change:

    git add .
    git commit -m "Update application"
    git push origin main

GitHub sends a webhook request to Jenkins.

Jenkins automatically starts a new build.

The pipeline then:

1. Checks out the latest source code.
2. Builds the Docker image.
3. Tags the Docker image.
4. Authenticates with Amazon ECR.
5. Pushes the Docker image to ECR.
6. The updated image can be deployed on EC2.

---

## 🔐 AWS IAM

AWS IAM was used to provide the Jenkins/EC2 environment with permissions required to interact with Amazon ECR.

ECR permissions used include:

- ecr:GetAuthorizationToken
- ecr:BatchCheckLayerAvailability
- ecr:GetDownloadUrlForLayer
- ecr:BatchGetImage
- ecr:InitiateLayerUpload
- ecr:UploadLayerPart
- ecr:CompleteLayerUpload
- ecr:PutImage

These permissions allow Jenkins to authenticate with ECR and push Docker images.

---

## 🧪 Project Verification

The CI/CD pipeline was successfully tested using GitHub Webhooks.

A GitHub push automatically triggered Jenkins.

Example Jenkins build:

    Build #10
    Started by GitHub push

The Docker image was successfully pushed to Amazon ECR.

The application was successfully deployed and verified on an AWS EC2 instance.

---

## 📸 Project Evidence

Recommended screenshots for this project:

### GitHub Repository

Show:

- Dockerfile
- Jenkinsfile
- index.html

### Jenkins Pipeline

Show a successful Jenkins build.

### GitHub Webhook

Show:

    Response: 200

### Amazon ECR

Show the Docker image and tag.

### Docker Container

Run:

    docker ps

Show the application container running.

### Web Application

Show the application running through the EC2 public IP.

---

## 🎯 Key DevOps Concepts Demonstrated

- Git & GitHub
- Source Code Management
- GitHub Webhooks
- CI/CD
- Jenkins Pipelines
- Jenkins Pipeline as Code
- Docker Containerization
- Docker Image Management
- Amazon ECR
- Amazon EC2
- AWS IAM
- Linux Administration
- Automated Build Triggers
- Container Deployment
- CI/CD Troubleshooting

---

## 💡 What I Learned

Through this project, I gained hands-on experience with:

- Creating Jenkins CI/CD pipelines
- Integrating GitHub with Jenkins
- Configuring GitHub Webhooks
- Writing Jenkinsfiles
- Building Docker images
- Managing Docker containers
- Working with Amazon ECR
- Configuring AWS IAM permissions
- Deploying containerized applications on EC2
- Troubleshooting Jenkins, Docker, Git, and AWS issues

---

## 🔮 Future Improvements

- Fully automate EC2 deployment from Jenkins
- Add automated testing
- Add Docker image versioning
- Add Docker image vulnerability scanning
- Add HTTPS using an Application Load Balancer
- Add CloudWatch monitoring
- Add deployment rollback support
- Use Amazon ECS/EKS for container orchestration

---

## 👨‍💻 Author

### Akash K

DevOps / AWS Enthusiast

Technologies demonstrated:

AWS · Linux · Git · GitHub · Jenkins · Docker · Amazon ECR · CI/CD
