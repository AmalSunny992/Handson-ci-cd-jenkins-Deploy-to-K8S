# Handson-ci-cd-jenkins-Deploy-to-K8S

This repository demonstrates a CI/CD pipeline using Jenkins to deploy a Java application to Kubernetes. 
The pipeline includes stages for code checkout, compilation, testing, static code analysis, dependency checking, packaging, deployment to Nexus, Docker image creation, security scanning, and deployment to Kubernetes.

## Repository Structure

- **Jenkinsfile**: Defines the Jenkins pipeline stages.
- **Dockerfile**: Defines the Docker image configuration for the application.
- **deploymentservice.yml**: Defines the Kubernetes deployment and service configurations.

## Jenkins Pipeline

The Jenkins pipeline defined in the `Jenkinsfile` includes the following stages:

### 1. Git Checkout
Checks out the code from the main branch of the repository.

### 2. Compile
Compiles the Java code using Maven.

### 3. Unit Test
Runs unit tests using Maven.

### 4. SonarQube Analysis
Performs static code analysis using SonarQube.

![image](https://github.com/user-attachments/assets/9ee7ebb2-61a0-4c0b-befd-96955a5da389)
![image](https://github.com/user-attachments/assets/f6741970-20b3-4229-8af5-c1b228cc4458)


### 5. OWASP Dependency Check
Checks for vulnerabilities in project dependencies.

### 6. Build
Packages the application into a JAR file.

### 7. Deploy To Nexus
Deploys the JAR file to a Nexus repository.

![image](https://github.com/user-attachments/assets/71e5f6f4-93d5-4552-9c37-56d2ffbf084c)
![image](https://github.com/user-attachments/assets/8a8a868f-64f1-4dc9-b41a-7f369f9ba18e)


### 8. Docker Build and Tag Image
Builds a Docker image for the application and tags it.

### 9. Trivy Scan
Scans the Docker image for vulnerabilities using Trivy.

### 10. Docker Push Image
Pushes the Docker image to Docker Hub.

![image](https://github.com/user-attachments/assets/53cdb2cd-f192-4e0d-b90d-4634a414e8fa)

### 11. Kubernetes Deploy
Deploys the application to a Kubernetes cluster using a deployment configuration file.

![image](https://github.com/user-attachments/assets/c787b438-0c81-478d-bbaa-8505b27d52a6)
![image](https://github.com/user-attachments/assets/758db047-2fa6-4013-9f83-fe2619a0b02e)
![image](https://github.com/user-attachments/assets/2c56fe7f-4249-4ab3-99ce-5fe34f7e906e)


Here is the Jenkinsfile used in this repository: [Jenkins File](./Jenkinsfile)


## Dockerfile
The Dockerfile defines the Docker image configuration for the application:

Here is the Dockerfile used in this repository: [Docker File](./docker/Dockerfile)

## Kubernetes Deployment File
The Kubernetes deployment file defines the deployment and service configurations for the application:

Here is the Kubernetes file used in this repository: [Deployment File](./kubernetes/deploymentservice.yml)

## Prerequisites
Jenkins server with the following plugins:
- Maven Integration
- Git
- SonarQube
- OWASP Dependency-Check
- Docker Pipeline
- Kubernetes CLI
- SonarQube server
- Nexus repository
- Docker Hub account
- Kubernetes cluster

## How to Use
- Clone this repository.
- Configure the Jenkins pipeline with the provided Jenkinsfile.
- Ensure the necessary credentials and tools are configured in Jenkins.
- Run the pipeline.

## License
This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.
