# Ekart Project

## Project Overview :
The Ekart Project is an e-commerce platform that allows users to browse and purchase a variety of products. This project showcases the use of modern CI/CD practices and tools to ensure high-quality code, secure software, and streamlined deployment processes.
![Alt Text](https://github.com/arfath29/Ekart-project/blob/master/Screenshot_18-6-2024_203723_www.youtube.com.jpeg)

## Key Features :
<<<<<<< HEAD
### User-Friendly Interface: 
A responsive and intuitive interface for a seamless shopping experience.
### Product Management: 
Features for adding, updating, and removing products.
### Order Processing: 
Efficient order management system for tracking and fulfilling orders.
### Security: 
Implemented various security measures to protect user data and ensure secure transactions.
## Technologies Used
### Java: 
Core backend development.
### Jenkins: 
Continuous Integration and Continuous Deployment (CI/CD) automation.
```bash
 $ sudo apt update
```
 ```bash
 $ sudo apt install openjdk-17-jre-headless
 ``` 
 ```bash
 $ sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
 ```
 ```bash
 $ echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ |  sudo  tee /etc/apt/sources.list.d/jenkins.list > /dev/null
 ```
```bash
 $ sudo apt install jenkins
```
 ```bash
 $ sudo systemctl start jenkins 
 $ sudo systemctl status jenkins
 ```
### SonarQube: 
Continuous inspection of code quality and security vulnerabilities.
```bash
$ apt install docker.io
```
```bash
$ docker run -d -p 9000:9000 sonarqube:lts-community
```
=======
### User-Friendly Interface:<span style="font-size:10px;"> A responsive and intuitive interface for a seamless shopping experience.
### Product Management: 
Features for adding, updating, and removing products.
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
>>>>>>> b4ac7b1bd17cc9230379dd35f0bd90694c6690ea

![Alt Text](https://github.com/arfath29/Ekart-project/blob/master/Screenshot_18-6-2024_203723_www.youtube.com.jpeg)
### Nexus:
Repository manager for storing and retrieving build artifacts.
```bash
$ docker run -d -p 8081:8081 sonatype/nexus3
$ docker exec -it <container id> /bin/bash
```
```bash
$ cd sonatype-work/nexus3
$ cat admin.password
```
![Alt Text](https://github.com/arfath29/Ekart-project/blob/master/Screenshot_13-6-2024_204116_15.207.72.196.jpeg)
### Maven: 
Dependency management and build automation.
### Docker: 
Containerization of the application for consistent and portable deployment.
### Kubernetes: 
Orchestration of Docker containers for scalable and resilient deployment.
## Setup K8-Cluster using kubeadm [K8 Version-->1.28.1]

### 1. Update System Packages [On Master & Worker Node]

```bash
sudo apt-get update
```

### 2. Install Docker[On Master & Worker Node]

```bash
sudo apt install docker.io -y
sudo chmod 666 /var/run/docker.sock
```

### 3. Install Required Dependencies for Kubernetes[On Master & Worker Node]

```bash
sudo apt-get install -y apt-transport-https ca-certificates curl gnupg
sudo mkdir -p -m 755 /etc/apt/keyrings
```

### 4. Add Kubernetes Repository and GPG Key[On Master & Worker Node]

```bash
curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
```

### Update Package List[On Master & Worker Node]

```bash
sudo apt update
```

### Install Kubernetes Components[On Master & Worker Node]

```bash
sudo apt install -y kubeadm=1.28.1-1.1 kubelet=1.28.1-1.1 kubectl=1.28.1-1.1
```

### Initialize Kubernetes Master Node [On MasterNode]

```bash
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
```

### Configure Kubernetes Cluster [On MasterNode]

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

### Deploy Networking Solution (Calico) [On MasterNode]

```bash
kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
```

### Deploy Ingress Controller (NGINX) [On MasterNode]

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
```


### Trivy:
Vulnerability scanner for containers.
```bash
$ sudo apt-get install wget apt-transport-https gnupg lsb-release
$ wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | sudo apt-key add -
$echo deb https://aquasecurity.github.io/trivy-repo/deb $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list.d/trivy.list
$ sudo apt-get update
$ sudo apt-get install trivy

```
## CI/CD Pipeline
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
## Pipeline 

```groovy

pipeline {
    agent any
    
    tools {
        jdk 'jdk17'
        maven 'maven3'
    }

    enviornment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
               git branch: 'main', credentialsId: 'git-cred', url: 'https://github.com/arfath29/Ekart-project.git'
            }
        }
        
        stage('Compile') {
            steps {
                sh "mvn compile"
            }
        }
        
        stage('Test') {
            steps {
                sh "mvn test"
            }
        }
        
        stage('File System Scan') {
            steps {
                sh "trivy fs --format table -o trivy-fs-report.html ."
            }
        }
        
        stage('SonarQube Analsyis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=BoardGame -Dsonar.projectKey=BoardGame \
                            -Dsonar.java.binaries=. '''
                }
            }
        }
        
        stage('Quality Gate') {
            steps {
                script {
                  waitForQualityGate abortPipeline: false, credentialsId: 'sonar-token' 
                }
            }
        }
        
        stage('Build') {
            steps {
               sh "mvn package"
            }
        }
        
        stage('Publish To Nexus') {
            steps {
               withMaven(globalMavenSettingsConfig: 'global-settings', jdk: 'jdk17', maven: 'maven3', mavenSettingsConfig: '', traceability: true) {
                    sh "mvn deploy"
                }
            }
        }
        
        stage('Build & Tag Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            sh "docker build -t adijaiswal/boardshack:latest ."
                    }
               }
            }
        }
        
        stage('Docker Image Scan') {
            steps {
                sh "trivy image --format table -o trivy-image-report.html adijaiswal/boardshack:latest "
            }
        }
        
        stage('Push Docker Image') {
            steps {
               script {
                   withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                            sh "docker push adijaiswal/boardshack:latest"
                    }
               }
            }
        }
        stage('Deploy To Kubernetes') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.8.146:6443') {
                        sh "kubectl apply -f deployment-service.yaml"
                }
            }
        }
        
        stage('Verify the Deployment') {
            steps {
               withKubeConfig(caCertificate: '', clusterName: 'kubernetes', contextName: '', credentialsId: 'k8-cred', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://172.31.8.146:6443') {
                        sh "kubectl get pods -n webapps"
                        sh "kubectl get svc -n webapps"
                }
            }
        }
}

}
```

