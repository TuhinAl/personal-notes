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

    What is Jobs in Jenkins?
    `Jobs` are the backbone of Jenkins. Job in Jenkins is any runnable task that is controlled or monitored by Jenkins.

    A job is a runnable task that is controlled or monitored by Jenkins. Jobs can be executed with parameters, on a specific node, at a specific time, and so on. Jobs can be chained, so that one job can trigger or wait for the completion of another. Jobs can be organized in a hierarchy of tasks.
    
    so Whatever the execution we are going to done by a Jenkins that execution must be done by a Jenkins Job. It means for each Execution task we need to create a Job in Jenkins.

    Create and Execute a Job in Jenkins:

**FreeStyle Project:**
This is a most common Type of Project, Build Type for this project is genenrally executed a shell(linux) command.

A FreeStyle Project in Jenkins is like a simple task list that you can set up to do specific jobs automatically. Imagine you have a robot that can do chores for you, like cleaning your room, doing your homework, and feeding your pet. You can tell the robot what to do and in what order.

In Jenkins, a FreeStyle Project is like giving instructions to that robot. You can tell Jenkins to:

1. Get the latest version of your code from a repository (like a library where your code is stored).
2. Build the code (like putting together a LEGO set).
3. Run tests to make sure everything works (like checking if the LEGO set is built correctly).
4. Deploy the code to a server (like putting the LEGO set on display).

Here's a real-world example:

Imagine you have a simple website, and you want to make sure it's always up-to-date and working correctly. You can create a FreeStyle Project in Jenkins to:

1. **Pull the latest website code** from GitHub.
2. **Build the website** (compile the code if needed).
3. **Run tests** to make sure the website works (check links, load pages, etc.).
4. **Deploy the website** to your hosting server.

This way, every time you make changes to your website code, Jenkins will automatically follow these steps to update your website without you having to do it manually.

In FreeStyle Project, we can run command in a shell/bash script, we can create the build of you software. or we can execute the script via freeStyle project.


**Pipeline Project:**
Its like a workflow. when we will create a complete workflow which will have some kind of Input, Output, and some kind of condition. then we will use the Pipeline Project. This project in normally written in DSL(Domain Specific Language).

A Pipeline in Jenkins is like a recipe that tells Jenkins how to build, test, and deploy your code. Think of it as a step-by-step guide that Jenkins follows to make sure everything is done correctly.

Here's an example to make it easy to understand:

Imagine you want to bake a cake. You have a recipe that tells you what to do step by step:

1. **Get the ingredients** (flour, sugar, eggs, etc.).
2. **Mix the ingredients** together.
3. **Bake the cake** in the oven.
4. **Decorate the cake** with frosting.

In Jenkins, a Pipeline is like this recipe. It tells Jenkins what steps to take to build, test, and deploy your code.

Here's a simple example of a Jenkins Pipeline:

```java
pipeline {
    agent any

    stages {
        stage('Get Ingredients') {
            steps {
                // Pull the latest code from GitHub
                git 'https://github.com/your-repo/your-java-project.git'
            }
        }
        stage('Mix Ingredients') {
            steps {
                // Build the project
                sh './gradlew build'
            }
        }
        stage('Bake the Cake') {
            steps {
                // Run tests
                sh './gradlew test'
            }
        }
        stage('Decorate the Cake') {
            steps {
                // Deploy the project
                sh './gradlew deploy'
            }
        }
    }
}
```

```go
pipeline {
    agent any

    stages {
        stage('Get Ingredients') {
            steps {
                // Pull the latest code from GitHub
                git 'https://github.com/your-repo/your-go-project.git'
            }
        }
        stage('Mix Ingredients') {
            steps {
                // Build the project
                sh 'go build ./...'
            }
        }
        stage('Bake the Cake') {
            steps {
                // Run tests
                sh 'go test ./...'
            }
        }
        stage('Decorate the Cake') {
            steps {
                // Deploy the project
                sh 'go install ./...'
            }
        }
    }
}
```

In this example:
- **Get Ingredients**: Jenkins pulls the latest code from GitHub.
- **Mix Ingredients**: Jenkins builds the project.
- **Bake the Cake**: Jenkins runs tests to make sure everything works.
- **Decorate the Cake**: Jenkins deploys the project to the server.

This way, Jenkins follows the Pipeline steps just like you would follow a recipe to bake a cake!

**Multi Configuration Project:**

As like FreeStyle Project, Multi Configuration Project is also a type of project in Jenkins. But the difference is that in FreeStyle Project we can run the build on only one platform. But in Multi Configuration Project we can run the build on multiple platforms.


**Execute Bash From Job:**
* create a shell file inside /tmp directory.
* write a shell script inside the file.
* Go to Job Configuration -> Build Steps -> Execute Shell -> write the path of the shell file with required parameter and click on Save.
* importantly, the shell file must have executable permission (chmod 755 FileName.sh).

Question: What is the way we can pass the parameter to the Jenkins Job at runtime? sothat I want to exexute a parameterize script. I want execute a script with different different parameter. How can I do that?
Ans: We can pass the parameter to the Jenkins Job at runtime by using the `Build with Parameters` option. In this option, we can pass the parameter to the Jenkins Job at runtime. 

**Parameterize Job:**

* Example: Job -> Configure -> General -> This project is parameterized -> Add Parameter -> String Parameter -> Name: `ENV` -> Default Value: `DEV` -> Apply -> Save.

**Anatomy of the Build**
#### Buildi Application Manually: get the application on Jenkins Machine:

There are some Lab in this section.

### Jenkins Plugins:
Jenkins Plugins are the building blocks of Jenkins. Jenkins Plugins are used to extend the functionality of Jenkins. Jenkins Plugins are used to integrate Jenkins with other tools. Jenkins Plugins are used to automate the process of Continuous Integration and Continuous Deployment. <br>
Plugins are basically enhance the core functionality of the software. Same case is also applicable for jenkins. Jenkins plugins are used to extend the functionality of Jenkins. Jenkins plugins are used to integrate Jenkins with other tools. Jenkins plugins are used to automate the process of Continuous Integration and Continuous Deployment. Jenkins plugins are used to automate the process of Continuous Integration and Continuous Deployment. <br>

Jenkins Core functionality is very limited. Jenkins Core functionality is limited to the following:
* Web Interface
* Job Scheduler
* Script Executor


**Running Jenkins with No Plugins:**
#### Installin and Using plugin
#### Standard Jenkins Build with Manual Plugin 
#### Jenkins Build Publish and Notify






















