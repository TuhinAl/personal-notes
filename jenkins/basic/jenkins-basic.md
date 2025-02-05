# Jenkins


## 1. Jenkins Beginners
### 1.1 Jenkins Basic
* 1.1.1 Jenkins Overview
* 1.1.2 Jenkins Installation and Running
* 1.1.3 FreeStyle Job/Project
* 1.1.4 Jenkins Configuration and Execution

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


### Jenkins Architecture:
* Jenkins Master and Slave:
    **Master Node:** Jenkins Server. Its work like a controller. It's responsible for scheduling build jobs, dispatching builds to the slaves for the actual job execution, monitoring the slaves (possibly taking them online and offline as required), and recording and presenting the build results. <br>
    
    **Slave Node:** Work as a Execution Node. Jenkins Slave is a Java executable that runs on a remote machine. Following are the key responsibilities of a Jenkins Slave:
        - Run build jobs dispatched by the Jenkins Master.
        - Monitor the execution of the build job.
        - Send the console output to the Jenkins Master.
        - Send the build result to the Jenkins Master.
        - Jenkins Master and Slave communicate via TCP/IP protocol.
        - Jenkins Master and Slave can be on the same machine or different machines.
        - Jenkins Master and Slave can be on the same network or different networks.

    * Single Master Node can have Multiple Slave Nodes.
    * Master Controls the load distribution to the Slave Nodes.
    * Jenkins UI is only available for the Master Node.
    * Java must be installed on the Slave Node. Please note that Jenkins installation is not required on the Slave Node. only and only Java is required on the Slave Node.
    * Master node connected with the Slave Node via SSH or Jenkins Agent.

    Continuous Integration (CI) is a software development practice in which developers regularly merge their code changes into a central repository, after which automated builds and tests are run. The key goals of continuous integration are to find and address bugs quicker, improve software quality, and reduce the time it takes to validate and release new software updates.

    What is JObs in Jenkins?
    A job is a runnable task that is controlled or monitored by Jenkins. Jobs can be executed with parameters, on a specific node, at a specific time, and so on. Jobs can be chained, so that one job can trigger or wait for the completion of another. Jobs can be organized in a hierarchy of tasks.
    
    
    Create and Execute a Job in Jenkins: