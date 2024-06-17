Ekart Project

Project Overview :
The Ekart Project is an e-commerce platform that allows users to browse and purchase a variety of products. This project showcases the use of modern CI/CD practices and tools to ensure high-quality code, secure software, and streamlined deployment processes.

Key Features :
User-Friendly Interface: A responsive and intuitive interface for a seamless shopping experience.
Product Management: Features for adding, updating, and removing products.
Order Processing: Efficient order management system for tracking and fulfilling orders.
Security: Implemented various security measures to protect user data and ensure secure transactions.
Technologies Used
Java: Core backend development.
Spring Boot: Framework for creating stand-alone, production-grade Spring-based applications.
Maven: Dependency management and build automation.
Docker: Containerization of the application for consistent and portable deployment.
Kubernetes: Orchestration of Docker containers for scalable and resilient deployment.
SonarQube: Continuous inspection of code quality and security vulnerabilities.
Trivy: Vulnerability scanner for containers.
Nexus: Repository manager for storing and retrieving build artifacts.

CI/CD Pipeline
The project includes a comprehensive Jenkins pipeline that automates the following stages:

1. Git Checkout: Cloning the project repository.
2. Compile: Compiling the project using Maven.
3. Test: Running unit tests to ensure code quality.
4. File System Scan: Scanning the file system for vulnerabilities using Trivy.
5. SonarQube Analysis: Performing static code analysis to detect bugs, code smells, and security vulnerabilities.
6. Quality Gate: Ensuring the code meets the quality standards set by SonarQube.
7. Build: Packaging the application using Maven.
8. Publish to Nexus: Deploying the build artifacts to a Nexus repository.
9. Build & Tag Docker Image: Creating and tagging Docker images.
10. Docker Image Scan: Scanning Docker images for vulnerabilities using Trivy.
11. Push Docker Image: Pushing Docker images to a Docker registry.
12. Deploy to Kubernetes: Deploying the application to a Kubernetes cluster.
13. Verify the Deployment: Ensuring the deployment is successful by checking the status of pods and services.
Access the Project
You can view the complete project on GitHub, which includes the source code, Jenkins pipeline script, Docker configurations, and Kubernetes deployment files.
