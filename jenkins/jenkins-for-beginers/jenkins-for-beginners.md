# Jenkins for Beginners Course:
### 1. Basics of CICD:

#### Understanding CICD:
![Understandin CICD](./image/understanding-cicd.png) <br>
In real time scenarios, you will often find multiple developers working on different feature branches, each focusing on a new enhancement. Performing multiple mergers without the implementation of continuous integration in a software development workflow can lead to several significant problems and challenges, such as delayed testing. So without CI testing typically occurs late in the development cycle, often after multiple mergers have taken place. This delay in testing can make it harder to identify and rectify issues early in the development process.
<br>
Challenges:<br>

![Need for CI](./image/need-for-CI.png) <br>

The CI pipeline proceeds through several stages, including unit testing, dependency scanning, artifact building, and vulnerability code scanning. All these assessments are performed on both the newly added code and the existing code from the main branch. If any of this test fails, the developer is asked to make necessary adjustments and commit the changes to the same old request. This action triggers the CI pipeline once again. <br>

![CI for feature branch A](./image/CI-process-A.png) <br>


Following the successful merge, The main branch now contains the code changes from both feature branch A and feature branch B and as mentioned earlier , any branch chanfe merge into the main branch automatically triggers a CI pipeline. It once afain runs all the tests including uni testing, dependency scanning, artifact building and vulnerability  scans.<br>

This ensures that the code changes from both feature branch B and A work seamlessly together. This entire process, which enables multiple developers to work on the same application, while ensuring that these new changes integrate smoothly without introducing any new issues, is known as continuous integration. <br>

![CI for feature branch B](./image/CI-B.png) <br>

### Continuous Deployment/Delivery:
Even after a rigorous CI and testing procedures, It is always advisable to deploy the modified application to a non production environment that closely resembles the live environemnt. This allows for live testinf before proceeding with production deployment.<br><br>

Within the feature branch. Following a successful CI pipeline run, we can establish another continuous deployment pipeline. This pipeline is responsible for deploying the modified code to a staging or, you know, development environment. Following deployment, a series of tests are executed to ensure the quality of the application. Upon successful completion of CD, the pull request is approved and merged back into the main branch.<br>

![CI for feature branch B](./image/CD.png) <br>

Within the main branch, the CA pipeline is triggered assessing the newly merged changes. If successful, it automatically initiates the CD pipeline resulting in the deployment of the application to the production environment. This automatic deployment process following successful continuous integration is referred to as continuous deployment. <br>
<br>
In certain instances, a manual approval step before production deployment is a critical aspect of the deployment process. This step ensures that it minimizes the risks, ensuring quality, adhering to the compliance requirements, and effectively coordinating changes. It basically offers a safety net, which allows for human judgment and oversight within an otherwise automated process. In this scenario, the following successful completion of the CI pipeline, The CT pipeline always awaits a human approval before proceeding with the production deployment. This process of manual approval prior to production deployment is known as  **continuous delivery** . <br>

## Jenkins Architecture:
**Intro:** Jenkins leverages a distributed architecture, which allows for the distribution of work across multiple machines. This architecture is composed of a master and multiple agents. The master is responsible for managing the entire Jenkins environment, including the configuration of jobs, security, and the distribution of work to the agents. The agents are responsible for executing the jobs assigned to them by the master. The agents can be configured to run on the same machine as the master or on a separate machine. This distributed architecture allows for the parallel execution of jobs, which can significantly reduce the time required to complete the build and test process. <br><br>

**1. Jenkins Controller**
The first component in the architecture is the Jenkins Controller. It is the central Hub of our jenkins setup, often referred to as the Jenkins Server. It has various responsiblities like management tasks such as user authentication, authorization, It can also manage jobs and pipelines like defining scheduling and monitoring the execution, it also provides web interface for configuration , setting up plugins, onboarding users, monitoring and managing the builds within the Jenkins. <br>
![CI for feature branch B](./image/JA-1.png) <br>
![CI for feature branch B](./image/JA-2.png) <br>
1. Prevent accidental damamge by keeping our controller configurations safe from potential job related changes.<br>
2. Boosts Perfomance by distributing build task across multipke machines, improving speed and effeciency for complex projects.<br>
3. Scaling up  the jenkins server by adding more nodes as a project and automation need increase,

**2. Node:** 
Node are also formarly known as Jenkins Slaved, so notes play a crucial role in your CID workflow by serving as the worker machine that execute our build jobs. Node are basically dedicated Linux, Windows or other machines that handle build execution, allowing for parallel processing and increased performance for large project.<br>
![CI for feature branch B](./image/JA-3.png) <br>
<br>
Node has a configurable number of **Executors**, which is the next component, which we will be talking about, which are essentially slots for running build jobs concurrently, and executor is a thread for execution of tasks. More executors allow for parallel processing of multiple jobs, which will help you to speed up the build process. 

<br>The number of executors assigned to a node is basically determined by the nodes available resources such as CPU and memory and the requirement of your build task. Ideally speaking, we allocate one executor for each note, which is the most secure setup. And if the task to be executed are small, assigning one executor per CPU core could be an effective approach as well.
<br><br>

**3. Agents** Agents act as an extension of Jenkins. Managing the task execution by using executors on a remote node. An agent represents a specific way a node connects to the controller. It defines the communication protocol and the authentication mechanism used.
For example, you might have a Java agent connecting, using JNLP or a SSH agent connecting,
using the secure shell protocol. Any tools required for the build and the test processes are installed on the node
where the agent runs. We can also leverage docker containers as build agents instead of installing tools and dependencies directly on a dedicated worker node. You can define a Docker image containing all the necessary software for your build jobs. And this is well suited for scenarios where build job requires specific software versions or have complex dependencies. Finally, when you're using a Docker agent, each build job runs in a clean, isolated container Ensuring consistent environments and preventing conflicts between multiple projects. Similarly, we can also utilize Kubernetes clusters to dynamically provision and manage build agents as ports. This allows for on demand scaling and efficient resource utilization. <br> <br>
![CI for feature branch B](./image/JA-4.png) <br>

So let's put it all together. Assume we have a Jenkins controller node connected to two worker nodes. You define jobs and pipelines within the controller using its UI, CLI or REST APIs.<br>
![CI for feature branch B](./image/JA-5.png) <br>
 The controller identifies available executors on connected nodes And then schedules and distributes jobs to the available executors on nodes.<br>
 ![CI for feature branch B](./image/JA-6.png) <br>
The nodes execute the jobs using the allocated resources.<br>
![CI for feature branch B](./image/JA-7.png) <br>
 Once the execution completes, the controller receives results and feedback from the nodes, providing the build status, the logs, and the artifacts. <br>
 ![CI for feature branch B](./image/JA-8.png) <br>
 This distributed architecture allows you to scale your Jenkins setup by adding more nodes with additional executors. This way you can handle complex workflows. and large project efficiently and ensuirng smooth and automated CICD pipelines. <br>

 ## Types of Jenkins Projects:
 Jenkins offer various project types also known as Jobs to automate different workflows.
 **Fressstyle Project:**
 It allows us to define custom builds steps and configurations for any project. It is the most flexible project type and can be used to create simple or complex build pipelines. <br>

**Pipeline Project:** It is a powerful approach, uses a specific code to define the entire build pipeline. It includes stages, steps and condition for complex build process and continuous delivery workflows. <br>

**Multibranch Pipeline:** 
Multi-branch pipelines build upon the pipeline projects by allowing you to manage builds from multiple branched in a single code repository. It's ideal for handling project with frequent branching and development activities. <br>

**Maven Project:**
Maven project  streamlined building projects that use Maven, a popular build automation tool for Java projects. It allows you to define Maven goals and options for building, testing and deploying your Java applications. Jenkins automatically detects and executes maven commands based on th POM.xml file<br>

**Multi Configuration Project:**
Multi configuration projects lets you run the same build process with different configurations. It's useful for testing your application across multiple environments, platforms, or versions. <br>

**Organizational Folder:** This aren't a project type themeselves, but rather a way to organize your Jenkins project into a hierarchical structure for better management, especially when dealing with a large number of project in addition ot the core types. It allows you to organize your Jenkins jobs into folders based on your organizational structure. It's useful for managing large number of jobs and pipelines. <br>
![CI for feature branch B](./image/project-type/project-type.png) <br>

### FreeStyle Project:
It allows you to define a series fo steps to be executed in a sequential order for automating tasks like building testing and deploying your project. The project often **chained** together. <br>
![CI for feature branch B](./image/project-type/free-style-project.png) <br>

So imagine building a mobile application. A freestyle project in Jenkins would be like a simple tool list for the build process. So you can have a project for cloning your code on running the unit test cases. You can have another project for building a docker image and publishing it to a container repository, and you can have a third project for Deploying the application. So it's like a simple to-do list with straightforward, basic tasks. <br><br>
![CI for feature branch B](./image/project-type/free-stype-limitation.png) <br>
**Limitations:** 

1. Project can only define steps in a simple sequence, even though they can be linked together via upstream and downstream jobs.
2. Configuration happens entirely through the graphical user interface, making it less flexible and centrally manageable. 
3. Modern continuous delivery pipelines often involve complex workflows that FreeStyle projects struggle to handle. Even achievable task might result in heavy, hard to maintain and unclear configurations. 

4. Many continuous delivery and deployment goals are simply not possible or become overtly complex with freestyle projects. 
5. **FreeStyle projects cannot be resumed after a Jenkins controller failure.**

In essence, freestyle projects are a **legacy approach**. While they might work for basic cases, they lack the flexibility and maintainability needed for most modern continuous delivery or deployments pipelines.

**Working with FreeStyle Job:**
1. **Creating a FreeStyle Job:** 
    - Click on **New Item** on the Jenkins dashboard.
    - Enter a name for the job and select **Freestyle Project**.
    - Click **OK** to create the job.
    - Configure the job by adding build steps, post build actions, and other settings.
    - Click **Save** to save the job configuration.
    - Click **Build Now** to run the job.