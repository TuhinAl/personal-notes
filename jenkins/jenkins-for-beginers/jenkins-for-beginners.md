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
Jenkins leverages a distributed architecture, which allows for the distribution of work across multiple machines. This architecture is composed of a master and multiple agents. The master is responsible for managing the entire Jenkins environment, including the configuration of jobs, security, and the distribution of work to the agents. The agents are responsible for executing the jobs assigned to them by the master. The agents can be configured to run on the same machine as the master or on a separate machine. This distributed architecture allows for the parallel execution of jobs, which can significantly reduce the time required to complete the build and test process. <br><br>

The first component in the architecture is the Jenkins Controller. It is the central Hub of our jenkins setup, often referred to as the Jenkins Server. It has various responsiblities like management tasks such as user authentication, authorization, It can also manage jobs and pipelines like defining scheduling and monitoring the execution, it also provides web interface for configuration , setting up plugins, onboarding users, monitoring and managing the bulds within the Jenkins. <br>
![CI for feature branch B](./image/JA-1.png) <br>