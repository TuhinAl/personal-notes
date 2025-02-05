# Jenkins


## 1. Jenkins Beginners
### 1.1 Jenkins Basic
* Jenkins Overview
* Jenkins Installation and Running
* FreeStyle Job/Project
* Jenkins Configuration and Execution

### 1.2 All about Jenkins Plugins
* Jenkins and Plugins Model
* Jenkins Plugin Installation
* Writing Custom Jenkins Plugin
* Managing and Upgrading Plugins

## 2 Jenlins Intermediate

### 2.1 Declarative Jenkins Pipeline
* Pipeline Introduction
* Jenkinfile Advanced
* Building Reusable Pipelines
* Using Pipeline for Workflow Execution


### 2.2 Building and Managing Multi-Node Jenkins Farm
* Setting Up Master Node
* Leverage Distributed Builds
* Building Pipeline Optimization
* Manage Distributed Build Farm
* Trigger Build Remotely

### 2.3 Running Jenkins in Docker
* Jenkins in Docker
* Creating Jenkins Build Farm with Docker
* MultiArchitecture Containers in Jenkins
* Maintaining Build Farm with Docker

### 2.4 Automate Jenkins with Groovy
* Fundamentals of Groovy
* Working with Jenkins and Groovy
* Creating builds with Groovy
* Working with Shared Libraries
* Managing Users and Credentials

## 3 Jenkins Advanced

### 3.1 Jenkins Modern CI/CD pipeline with Jenkins
* Jenkins Scripted Pipeline
* Building and Testing Code
* Integrate container Security Complience
* Complete End-To-End CI/CD Pipeline for our Application


### 3.2 Jenkins X for CI/CD
* Jenkins X and Setup
* Quick Start with jenkins X
* Managing Env with GitOps
* Build Packers adn Pipelines
* Versioning and Releasing Application

### Jenkins Security


Jenkins Installation in Docker:
Step-1: Create a volume for Jenkins Home
    `$ docker volume create jenkins_data`

Step-2: Run Jenkins Docker
```
docker run -d \
  --name jenkins \
  -p 8080:8080 -p 50000:50000 \
  -v jenkins_data:/var/jenkins_home \
  -u root \
  --restart unless-stopped \
  jenkins/jenkins:lts
  ```
  
Step-3: Access Jenkins UI: `http://localhost:8080`
Step-4: Get Password:
`$ docker logs jenkins | grep "Admin password"`
