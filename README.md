# jenkins-lab..Digi Jenkins Lab 2 - Secure CI/CD Pipeline Implementation
Overview

This project demonstrates the implementation of a complete CI/CD workflow using Jenkins, Docker, SonarQube, and Trivy. The objective is to automate code integration, quality validation, security scanning, containerization, and deployment while following DevOps best practices.

Objectives
Automate application delivery using Jenkins.
Perform continuous code quality inspection with SonarQube.
Detect security vulnerabilities using Trivy.
Build and manage Docker containers efficiently.
Push versioned images to Docker Hub.
Deploy the application automatically after successful validation.
CI/CD Workflow

The pipeline executes the following sequence:

1. Source Code Retrieval

Jenkins securely connects to a private GitHub repository using Personal Access Token (PAT) credentials and retrieves the latest code from the main branch.

2. Code Quality Analysis

SonarQube scans the application source code to identify:

Bugs
Code smells
Security issues
Maintainability concerns
3. Quality Gate Verification

The pipeline waits for SonarQube's Quality Gate result. The build proceeds only if the defined quality standards are met.

4. Container Build

A Docker image is created from the application source code and tagged dynamically using the Jenkins build number.

5. Security Assessment

Trivy performs a vulnerability scan on the generated Docker image. The pipeline is configured to detect critical security vulnerabilities before deployment.

6. Image Publication

After passing all checks, the Docker image is uploaded to Docker Hub using secure Jenkins credentials.

7. Automated Deployment

The application container is deployed and exposed on port 8081.

8. Cleanup Tasks

Unused Docker images and temporary resources are removed to maintain a clean build environment.

Technologies Used
Technology	Purpose
Jenkins	CI/CD Orchestration
GitHub	Source Control Management
SonarQube	Code Quality Analysis
Docker	Containerization Platform
Trivy	Container Security Scanning
PHP 8.2	Application Runtime
Docker Hub	Container Registry
Repository Layout
digi-jenkins-lab/
│
├── Jenkinsfile
├── Dockerfile
├── sonar-project.properties
├── index.php
│
├── src/
│   ├── OrderProcessor.php
│   └── SubscriptionManager.php
│
├── tests/
│   ├── OrderTest.php
│   └── SubscriptionTest.php
│
└── screenshots/
Key Components
File/Folder	Description
Jenkinsfile	Pipeline automation script
Dockerfile	Docker image configuration
sonar-project.properties	SonarQube project settings
src/	Application source code
tests/	Unit testing resources
screenshots/	Evidence and lab screenshots
Environment Prerequisites

Before running the project, ensure the following components are installed:

Ubuntu 22.04 or later
OpenJDK 17+
Docker Engine
Jenkins Server
SonarQube Community Edition
Trivy Security Scanner
Git
Jenkins Credential Configuration

The following credentials must be created in Jenkins:

Credential ID	Type	Usage
github-pat-creds	Username & Password	Access private GitHub repository
dockerhub-creds	Username & Password	Push images to Docker Hub
sonar-token	Secret Text	Authenticate with SonarQube
Deployment Instructions
Clone the Repository
git clone <repository-url>
cd digi-jenkins-lab
Configure Jenkins
Create a new Pipeline Job.
Connect the job to the repository.
Select branch:
*/main
Add all required credentials.
Save the configuration.
Start the Pipeline

From Jenkins Dashboard:

Build Now

Monitor each stage through the Jenkins Console Output.

Docker Image Information

Docker Hub Repository:

ahmed30103/service-app

Image Tag Format:

ahmed30103/service-app:<build-number>

Example:

ahmed30103/service-app:15
Application Access

Once deployment is completed successfully, access the application through:

http://<VM_IP>:8081

Example:

http://192.168.1.100:8081
Security Features
Private GitHub repository integration
Secure credential storage in Jenkins
SonarQube Quality Gate enforcement
Trivy vulnerability scanning
Automated cleanup of local Docker images
Expected Outcome

After a successful pipeline execution:

✅ Source code is retrieved from GitHub
✅ Code quality is validated by SonarQube
✅ Security scan is completed using Trivy
✅ Docker image is built successfully
✅ Image is pushed to Docker Hub
✅ Application is deployed automatically
✅ Build environment is cleaned up
