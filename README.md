# Netflix Clone Deployment
Netflix clone using various tools and technologies. Jenkins will serve as the Continuous Integration and Continuous Deployment (CICD) tool, and the application will be deployed within a Docker container, managed within a Kubernetes Cluster. Additionally, for monitor Jenkins and Kubernetes metrics using Grafana, Prometheus, and Node exporter.

## GitHub Repository

[GitHub Repository](https://github.com/sirishacyd/netflix-clone)


![architecture ](screenshots/)

## Steps

### Step 1: Launch an Ubuntu(22.04) T2 Large Instance

- Start by launching an Ubuntu 22.04 T2 Large instance on preferred cloud provider.

### Step 2: Install Jenkins, Docker, and Trivy. Create a Sonarqube Container using Docker.

- Install Jenkins, Docker, and Trivy on your server.
- Create a Sonarqube container using Docker.

### Step 3: Create a TMDB API Key

- Obtain a TMDB API Key for accessing movie data.

### Step 4: Install Prometheus and Grafana On the new Server

- Install Prometheus and Grafana on your server for monitoring.

### Step 5: Install the Prometheus Plugin and Integrate it with the Prometheus server

- Set up Prometheus plugin and integrate it with your Prometheus server for metrics collection.

### Step 6: Email Integration With Jenkins and Plugin setup

- Configure email integration with Jenkins and set up necessary plugins.

### Step 7: Install Plugins like JDK, Sonarqube Scanner, Node.js, and OWASP Dependency Check

- Install required plugins such as JDK, Sonarqube Scanner, Node.js, and OWASP Dependency Check in Jenkins.

### Step 8: Create a Pipeline Project in Jenkins using a Declarative Pipeline

- Create a pipeline project in Jenkins using a declarative pipeline to automate your deployment.

### Step 9: Install OWASP Dependency Check Plugins

- Install OWASP Dependency Check plugins for security scanning.

### Step 10: Docker Image Build and Push

- Build and push Docker images for your application.

### Step 11: Deploy the image using Docker

- Deploy the Docker image of your application.

### Step 12: Kubernetes master and slave setup on Ubuntu (20.04)

- Set up a Kubernetes master and slave on Ubuntu 20.04 for scalable deployment.

### Step 13: Access the Netflix app on the Browser

- Access your Netflix clone application through a web browser.

### Step 14: Terminate the AWS EC2 Instances

- Terminate the AWS EC2 instances to save resources.


## let's get started and dig deeper into each of these steps:

## Step 1: Launch an Ubuntu(22.04) T2 Large Instance

Launch an AWS T2 Large Instance, using the Ubuntu image. You have the option to either create a new key pair or use an existing one. For the purpose of learning, enable HTTP and HTTPS settings in the security group and open all ports

![ec2](screenshots/netflix-ec2.png)

## Step 2: Install Jenkins, Docker, and Trivy

### 2A: To Install Jenkins

Connect to your console, and enter these commands to Install Jenkins

```
vi jenkins.sh #make sure run in Root (or) add at userdata while ec2 launch
```

```
#!/bin/bash
sudo apt update -y
#sudo apt upgrade -y
wget -O - https://packages.adoptium.net/artifactory/api/gpg/key/public | tee /etc/apt/keyrings/adoptium.asc
echo "deb [signed-by=/etc/apt/keyrings/adoptium.asc] https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | tee /etc/apt/sources.list.d/adoptium.list
sudo apt update -y
sudo apt install temurin-17-jdk -y
/usr/bin/java --version
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
                  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
                  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
                              /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update -y
sudo apt-get install jenkins -y
sudo systemctl start jenkins
sudo systemctl status jenkins
```
