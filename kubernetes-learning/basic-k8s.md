
[K8s Concept](https://kubernetes.io/docs/concepts/)

# Why you need Kubernetes and what it can do? 
##### Kubernetes is a portable, extensible, open source platform for managing containerized workloads and services, that facilitates both declarative configuration and automation. It has a large, rapidly growing ecosystem. Kubernetes services, support, and tools are widely available.

Containers are a good way to bundle and run your applications. In a production environment, you need to manage the containers that run the applications and ensure that there is no downtime. For example, if a container goes down, another container needs to start. Wouldn't it be easier if this behavior was handled by a system?

That's how Kubernetes comes to the rescue! Kubernetes provides you with a framework to run distributed systems resiliently. It takes care of scaling and failover for your application, provides deployment patterns, and more. For example: Kubernetes can easily manage a canary deployment for your system.

Kubernetes provides you with:
* **Service discovery and load balancing:** Kubernetes can expose a container using the DNS name or using their own IP address. If traffic to a container is high, Kubernetes is able to load balance and distribute the network traffic so that the deployment is stable.
* **Storage orchestration:** Kubernetes allows you to automatically mount a storage system of your choice, such as local storages, public cloud providers, and more.
* **Automated rollouts and rollbacks:** You can describe the desired state for your deployed containers using Kubernetes, and it can change the actual state to the desired state at a controlled rate. For example, you can automate Kubernetes to create new containers for your deployment, remove existing containers and adopt all their resources to the new container.

* **Automatic bin packing:**
* **Self-healing:** Kubernetes restarts containers that fail, replaces containers, kills containers that don't respond to your user-defined health check, and doesn't advertise them to clients until they are ready to serve.

* **Secret and configuration management:**
* **Horizontal scaling:**
* **IPv4/IPv6 dual-stack:**
* **Designed for extensibility** Add features to your Kubernetes cluster without changing upstream source code.



# [Pods](https://kubernetes.io/docs/concepts/workloads/pods/)

* Pods are the smallest deployable units of computing that you can create and manage in Kubernetes.
* A Pod is a group of one or more containers, with shared storage and network resources, and a specification for how to run the containers. 
* A Pod models an application-specific "**logical host**": it contains one or more application containers which are relatively tightly coupled.

* As well as application containers, a Pod can contain **init containers** that run during Pod startup. You can also inject **ephemeral containers** for debugging a running Pod.
* init containers: One or more initilization containers that must run to completion before any app containers run.
* ephemeral containers: Debugging containers that can be added to a running Pod to troubleshoot the application. or we can say A type of container that we can temporarily run inside a pod.
* A Pod is similar to a set of containers with shared namespaces and shared filesystem volumes.
* Pods in a Kubernetes cluster are used in **two** main ways:
    1. **Pods that run a single container.** A Pod is a wrapper around a single container; Kubernetes manages Pods rather than managing the containers directly.
    2. Pods that run multiple containers that need to work together.

* Usually we don't need to create Pods directly, even singleton Pods. Instead, create them using workload resources such as **Deployment** or **Job**. If your Pods need to track state, consider the **StatefulSet** resource.
    1. **Deployment:** Manages a replicated Application on out cluster.
    2. **Job:** A finite or batch task that runs to completion.
    3. **StatefulSet:** Manages stateful applications. A StatefulSet manages deployment and scaling of a set of Pods, with durable storage and persistent identifiers for each Pod.

* Each Pod is meant to run a single instance of a given application. If we want to scale our application horizontally (to provide more overall resources by running more instances), we should use multiple Pods, one for each instance. In Kubernetes, this is typically referred to as **replication**. Replicated Pods are usually created and managed as a group by a workload resource and its controller.

* Pod gets created by Controller.
* Restarting a container in a Pod should not be confused with restarting a Pod. A Pod is not a process, but an environment for running container(s). A Pod persists until it is deleted.
* The name of a Pod must be a valid DNS subdomain value, but this can produce unexpected results for the Pod hostname. For best compatibility, the name should follow the more restrictive rules for a DNS label.

* A [controller](https://kubernetes.io/docs/concepts/workloads/) for the resource handles replication and rollout and automatic healing in case of Pod failure. For example, if a Node fails, a controller notices that Pods on that Node have stopped working and creates a replacement Pod. 

    Here are some examples of workload (A workload is an application running on Kubernetes) resources that manage one or more Pods:
    1. [Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)
    2. [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)
    3. [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)

* **PodTemplates** are specifications for creating Pods, and are included in workload resources such as Deployments, Jobs, and DaemonSets.
### Deployment Related notes:

Rolling Update and Rollback:
* Kubernetes supports rolling updates for Deployments, StatefulSets, and DaemonSets.
* A rolling update gradually replaces Pods with new ones, without downtime.
* A rollback is a way to revert to a previous version of a Deployment, StatefulSet, or DaemonSet.
* Kubernetes automatically creates a new ReplicaSet for each new Deployment revision.
* You can use the kubectl rollout command to manage the rollout of a Deployment, StatefulSet, or DaemonSet.
`kubectl rollout restart deployment <deployment-name>`  
This command restarts the specified Deployment by rolling out a new version of its Pods. Replace `<deployment-name>` with the name of your Deployment.
* You can use the kubectl rollout status command to view the status of a Deployment, StatefulSet, or DaemonSet.
   `kubectl rollout status deployment <deployment-name>`
This command shows the status of the specified Deployment's rollout. Replace `<deployment-name>` with the name of your Deployment.
* You can use the kubectl rollout undo command to revert to a previous version of a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout undo deployment <deployment-name>`
* You can use the kubectl rollout history command to view the history of a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout history deployment <deployment-name>` 
* You can use the kubectl rollout status command to view the status of a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout status deployment <deployment-name>` 
* You can use the kubectl rollout pause command to pause a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout pause deployment <deployment-name>`
* You can use the kubectl rollout resume command to resume a paused Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout resume deployment <deployment-name>`
* You can use the kubectl rollout restart command to restart a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout restart deployment <deployment-name>`
* You can use the kubectl rollout scale command to scale a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout scale deployment <deployment-name> --replicas=<number-of-replicas>`
* You can use the kubectl rollout history command to view the history of a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout history deployment <deployment-name>`
* You can use the kubectl rollout undo command to revert to a previous version of a Deployment, StatefulSet, or DaemonSet.
    `kubectl rollout undo deployment <deployment-name>` 