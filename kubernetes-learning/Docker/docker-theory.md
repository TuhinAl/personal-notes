Docker Container Lifecycle: A container is a self-contained, isolated environment that encapsulates a set of processes and their dependencies. Containers only lives as long as the process is running. Once the process stops, the container automatically stops.

1. Container Creation: docker run <image>
2. Container Start: docker start <container>
3. Container Stop: docker stop <container>
4. Container Pause: docker pause <container>
5. Container Unpause: docker unpause <container>
6. Container Kill: docker kill <container>
7. Container Delete: docker rm <container>
8. Container Run: docker run -d -p 80:80 --name my-nginx nginx 
9. Container Exec: docker exec -it my-nginx bash
docker exec container_id cat /etc/hosts : to print the hosts file content 

run attached mode: docker run -d -p 80:80 --name my-nginx nginx
run detached mode: docker run -d -p 80:80 --name my-nginx nginx

Ports Mapping:
1. Host to Container: docker run -d -p 80:80 --name my-nginx nginx
2. Container to Host: docker run -d -p 80:80 --name my-nginx nginx
3. Container to Container: docker run -d --name my-nginx1 nginx


Volume Mapping:
Volume Mapping: Volume mapping is a mechanism to mount a host directory into a container. It allows you to share files between the host and the container. This is useful when you want to share data between the host and the container, such as configuration files or data files. 

Volume mapping read only mode: docker run -d -p 80:80 -v /var/www/html:/var/www/html:ro --name my-nginx nginx

1. Host to Container: docker run -d -p 80:80 -v /var/www/html:/var/www/html --name my-nginx nginx
2. Container to Host: docker run -d -p 80:80 -v /var/www/html:/var/www/html --name my-nginx nginx
3. Container to Container: docker run -d -v /var/www/html:/var/www/html --name my-nginx1 nginx

Docker Image Lifecycle:
1. Image Creation
2. Image Push
3. Image Pull
4. Image Delete

Docker Volume Lifecycle:
1. Volume Creation
2. Volume Mount
3. Volume Unmount
4. Volume Delete

Docker Network Lifecycle:
1. Network Creation
2. Network Connect
3. Network Disconnect
4. Network Delete

Docker Service Lifecycle:
1. Service Creation
2. Service Start
3. Service Stop
4. Service Delete

Docker Swarm Lifecycle:
1. Swarm Init
2. Swarm Join
3. Swarm Leave
4. Swarm Unlock
5. Swarm Lock
6. Swarm Unlock
7. Swarm Unlock
8. Swarm Unlock

Docker Compose Lifecycle:
1. Compose Create
2. Compose Start
3. Compose Stop
4. Compose Remove

Docker Registry Lifecycle:
1. Registry Creation
2. Registry Push
3. Registry Pull
4. Registry Delete

Docker Stack Lifecycle:
1. Stack Create
2. Stack Start
3. Stack Stop
4. Stack Remove

Docker Machine Lifecycle:
1. Machine Create
2. Machine Start
3. Machine Stop
4. Machine Remove

Docker Plugin Lifecycle:
1. Plugin Install
2. Plugin Uninstall

Docker Secret Lifecycle:
1. Secret Create
2. Secret Remove

Docker Config Lifecycle:
1. Config Create
2. Config Remove

Docker Network Driver Lifecycle:
1. Network Driver Create
2. Network Driver Remove

Docker Volume Driver Lifecycle:
1. Volume Driver Create
2. Volume Driver Remove



2. Network Driver Remove

Docker Volume Driver Lifecycle:
1. Volume Driver Create
2. Volume Driver Remove


### Docker Engine

Docker Engine is the core component of Docker, responsible for creating and running containers. It consists of three main components:
1. **Docker Daemon**: The background service running on the host that manages Docker containers.
2. **Docker Client**: The command-line interface (CLI) that allows users to interact with the Docker Daemon.
3. **REST API**: An API that allows programs to communicate with the Docker Daemon.

### Docker Service configuration

Check docker

### Docker Service configuration

Check docker service status: `systemctl status docker` <br>

when a docker daemon run its listen on a **Unix Socket**. The default location for the Unix socket is `/var/run/docker.sock`. <br>
Uinix Socket is an IPC (Inter-Process Communication) mechanism that allows communication between processes on the same host. <br> Docker daemon is accessible only from the host where it is running. <br> becuase it is only listening on the Unix socket. <br> we could make docker daemon listen on a TCP Interface on the docker host by adding host opttion.

`
dockerd --debug \ 
        --host tcp://192.168.1.10:2375 \
`

now the docker daemon is accessible from the remote host using the IP  192.168.1.10<br>

Other host can connect to the docker daemon by setting an environment variable: <br>
export DOCKER_HOST="tcp://192.168.1.10:2375" <br>

you must be extreamly careful when exposing the docker daemon over the network because the default configuration does not have any **authentication or encryption**
By default docker daemon serve unencrypted traffic over the network. <br>

Question: what if we need to establish a connection to the Docker daemon from a remote host? <br>
Ans: **TCP Socket** : To allow remote connections to the Docker daemon, you need to enable the TCP socket. This can be done by modifying the Docker daemon configuration file. <br>




**TLS Encryption:** To secure the communication between the Docker client and the Docker daemon, you can enable TLS encryption. This requires generating TLS certificates and configuring the Docker daemon to use them. <br>

To enable TLS encryption, you must first create a pair of TLS certificate and the TLS flag true, pass in the path to the certificate and key files. To enable TLS, the standard port is 2376 instead of 2375. <br>

```docker --debug \
       --host=tcp://192.168.1.10:2376 \
       --tls=true \
       --tlscert=/var/docker/tls/server-cert.pem \
       --tlskey=/var/docker/tls/server-key.pem \
```

as of now, this command could be moved to configuration file `/etc/docker.daemon.json` <br>

`{
    "debug": true,
    "hosts": ["tcp://192.168.1.10:2376"], // support multiple listeners
    "tls": true,
    "tlscert": "/var/docker/tls/server-cert.pem",
    "tlskey": "/var/docker/tls/server-key.pem"
}
`

#### Basic contianer operations


![Docker Objects](./images/engine/docker-objects.png)

`$ docker <docker-object> <subcommand> <options> <arguments/Commands>`

all images and container exist in the docker host `/var/lib/docker/` 

#### Docker container basic operations
 * Create a container: `docker create <image>`
    * Start a container: `docker start <container>`
    * Stop a container: `docker stop <container>`
    * Pause a container: `docker pause <container>`
    * Unpause a container: `docker unpause <container>`
    * Kill a container: `docker kill <container>`
    * Delete a container: `docker rm <container>`
    * Run a container: `docker run <image>`
    * Execute a command in a running container: `docker exec <container> <command>`
    * Attach to a running container: `docker attach <container>`
    * Inspect a container: `docker inspect <container>`
    * List running containers: `docker ps`
    * List all containers: `docker ps -a`
    * List container logs: `docker logs <container>`
    * List container processes: `docker top <container>`
    * Copy files to/from a container: `docker cp <source> <destination>`
    * Export a container: `docker export <container>`
    * Import a container: `docker import <file>`
    * Rename a container: `docker rename <container> <new-name>`
    * Update a container: `docker update <container>`
    * Wait for a container to exit: `docker wait <container>`
    * Resize a container's TTY: `docker resize <container>`
    * Inspect changes to a container's filesystem: `docker diff <container>`

    
#### Container Inspect:
`docker inspect <container>` // resource consumption of the container <br>
docker logs <container> // logs of the container <br>

docker container logs -f <container> // follow the logs of the container <br>

#### Stopping and removing containers
 **Linux Signals:**
    1. SIGTERM: This signal is used to request a process to terminate. It allows the process to perform cleanup operations before exiting.
    2. SIGKILL: This signal is used to forcefully terminate a process. It does not allow the process to perform any cleanup operations.
    3. SIGINT: This signal is used to interrupt a process. It is typically sent by pressing Ctrl+C in the terminal.
    4. SIGQUIT: This signal is used to request a process to quit. It is similar to SIGINT but produces a core dump when the process exits.
    5. SIGHUP: This signal is used to hang up a process. It is typically used to reload configuration files or restart daemons.
    6. SIGUSR1: This signal is a user-defined signal that can be used by applications to perform custom actions.
    7. SIGUSR2: This signal is another user-defined signal that can be used by applications to perform custom actions.
    8. SIGWINCH: This signal is used to notify a process that the terminal window size has changed.
    9. SIGSTOP: This signal is used to stop a process. It suspends the process and can be resumed later using the SIGCONT signal.
    10. SIGCONT: This signal is used to resume a process that has been stopped using the SIGSTOP signal.
    `$ kill -SIGSTOP $(pgrep nginx)` // stop the nginx process
    `$ docker container kill --signal=9 web` // kill the container with the signal 9
    `$ ls -lrt /var/lib/docker/containers/` // list all the containers in the docker host
    `$ docker container ls -q` // list all the containers in the docker host
    `$ docker container stop $(docker container ls -q)` // stop all the containers in the docker host
    `$ docker container rm -f $(docker container ls -aq)` // remove all the containers in the docker host

ifter loging in container with interactive terminal mode, using `ps -ef` command to list all the process in the container. <br>
`$ docker exec -it <container> bash` <br>
`$ ps -ef` <br>
`$ tty` - print the file name of the terminal connected to standard input <br>
`$ exit` - exit the container <br>
`$ Ctrl+P+Q` - exit the container without stopping the container <br>
![Container Process](./images/engine/container-process.png) <br>

`$ docker exec -it <container> hostname` <br> // print the hostname of the container <br>
`$ docker exec -it <container> cat /etc/hosts` <br> // print the hosts file content <br>
`$ docker exec -it d7 cat /etc/lsb-release` <br> // print the os version of the container <br>

`$ docker exec -it <container> cat /etc/os-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/issue` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/lsb-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/redhat-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/debian_version` <br> // print the os version of the container <br>

`$ docker exec -it <container> cat /etc/issue` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/lsb-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/redhat-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/debian_version` <br> // print the os version of the container <br>

`$ docker exec -it <container> cat /etc/issue` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/lsb-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/redhat-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/debian_version` <br> // print the os version of the container <br>

`$ docker exec -it <container> cat /etc/issue` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/lsb-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/redhat-release` <br> // print the os version of the container <br>
`$ docker exec -it <container> cat /etc/debian_version` <br> //

`$ docker container log -f <container>` // follow the live-logs of the container <br>

#### Set hostname
`$ docker run -d --name my-nginx --hostname my-nginx nginx` <br>
`$ docker exec -it my-nginx hostname` <br>

#### Restart policy
`$ docker run -d --name my-nginx --restart always nginx` <br>
`$ docker run -d --name my-nginx --restart unless-stopped nginx` <br>
`docker run -d --name my-nginx --restart on-failure:5 nginx` <br>
Catch: It does not restart the container if the container is stopped manually. it restart if the daemon is restarted. <br>
![Container Restart Policy](./images/engine/container-restart-policy.png)


**Live Restore in Docker:** Live restore is a feature that allows Docker to restore containers that were running when the Docker daemon was stopped or restarted. This feature is useful for maintaining the state of containers across daemon restarts (for unless-stopped). <br>
`$ docker run -d --name my-nginx --live-restore nginx` <br>
docker live restore is configured in the docker daemon configuration file. <br>
`/etc/docker/daemon.json` <br>
`{
    "live-restore": true
}` <br>
and then restart the docker service
`systemctl restart docker` <br>
`systemctl start docker` <br>


Copying files to and from a container: <br>
* Container cp-- from **host to container** <br>
`$ docker container cp <source> <destination>` <br>
example: `docker container cp /etc/hosts my-nginx:/tmp/hosts` <br>

* Container cp-- from **container to host** <br>
`$ docker container cp <container>:<source> <destination>` <br>

`$ docker cp /etc/hosts my-nginx:/tmp/hosts` <br>
`$ docker exec -it my-nginx cat /tmp/hosts` <br>
`$ docker cp my-nginx:/tmp/hosts /tmp/hosts` <br>

![Container Restart Policy](./images/engine/copying-contents.png) <br>

#### Publishing port and port mapping:
1. **Host to Container**: `docker run -d -p 80:80 --name my-nginx nginx` <br>
2. **Container to Host**: `docker run -d -p 80:80 --name my-nginx nginx` <br>
3. **Multiple Network Interfaces**: 
Suppose our host hase 3 different network interfaces, and we want to bind the container to a specific network interface. <br>
`$ docker run -d -p 192.168.1.5:80:80 --name my-nginx nginx` <br>
`$ docker run -d -p 127.0.0.1:80:80 --name my-nginx nginx` <br>
`$ docker run -d -p 5000:80 --name my-nginx nginx`  //omit the host ip  and port<br>
ephemeral port range: 32765 - 60999
these ports are defined in:  <br>
`$ cat /proc/sys/net/ipv4/ip_local_port_range` <br>
Ephemeral port range is used by the kernel to assign the port to the application. Ephemeral port range is a set of temporary ports used by networking protocol software for establishing outgoing connections

![Container Port Mapping](./images/engine/port-mapping.png) <br>
![Container Port Publish](./images/engine/port-publish.png) <br>

#### How does docker map a port? 
Using IpTables Rules: <br>
Ip Tables Rules: used to manage packet filtering rules and NAT rules in the Linux kernel firewall. <br>
`$ iptables -t nat -L -n`
`$ iptables -t nat -S DOCKER` <br>

#### Docker container part2:
`docker container run -itd --name=testcontainer --rm ubuntu` used in CICD pipeline, when many containers are created and destroyed simultaneously. <br> 

The main difference between docker name and hostname is that the name is used to identify the container in the docker host, while the hostname is used to identify the container in the network. docker name must be unique but hostname can be the same for multiple containers <br>

**exploring --restart 4 cases**
`$ docker container run -itd --name=caseone --restart=no ubuntu` <br>
`$ docker container run -itd --name=casetwo --restart=on-failure ubuntu` <br> // in this situation, the container will restart if it exits with it non-zero exit status
`$ docker container run -itd --name=casethree --restart=always ubuntu` <br> // restart if docker daemon restart
`$ docker container run -itd --name=casefour --restart=unless-stopped ubuntu` <br>
In this case: docker container will NOT restart even though docker daemon is restart

`$ ls -lrt /var/lib/docker/containers/` <br> // list all the containers in the docker host <br>


## Docker Image Management

 [Kapeli Dockerfile Guide](https://kapeli.com/cheat_sheets/Dockerfile.docset/Contents/Resources/Documents/index/ )

docker login docker.io <br>
docker pull ubuntu:latest <br>
#### image retagging and pushing
`$ docker tag httpd:alpine httpd:customv1` <br>
`$ docker push myrepo/httpd:customv1` <br>
`$ docker push privaterepo.com/myrepo/httpd:customv1` <br>  push the image to the private repository <br>
`$ docker system df` <br> will display the actual size of different object

docker image history <image> <br> // display the history of the image or image layers <br>

**Images inspect -with format**
`$ docker image inspect httpd -f '{{.Os}}'` <br>  print the os of the image <br>
`$ docker image inspect httpd -f '{{.Architecture}}'`  
`$ docker image inspect httpd -f '{{.Architecture}} {{.Os}}'`  

Image Save and Load: <br>
`$ docker image save alpine:latest -o alpine.tar`
`$ docker image load -i httpd.tar` <br>

`$ docker image tag httpd:alpine httpd:test1` //
`$ docker system df` // verify actual size of the docker images

`$ docker image save httpd:latest -o httpd.tar `<br>
`$ docker image load -i httpd.tar` <br> // this approach is used to save the image and load the image in the different docker host if the internet is not available

`$ docker export test > httpd.tar`  export the container to the tar file to create images
`$ docker image import httpd.tar httpd:lates`

#### Create docker images
`$ docker build . -f Dockerfile -t tuhinal/my-app:latest` <br>
`$ docker push tuhinal/my-app:latest`

ls -lrt

## Docker Security

#### Docker Daemon Security: 
What is the problem if someone gets access to the docker daemon? <br>
* Can delete existing containers hosting application
* Delete volumes storing data
* Run container to run their application (i.e bitcoin mining)
* Gain root access to the host system by running a previleged container.
* Target the other systems in the network.

By Default Docker exposes the docker daemon service within the host only one UNIX Socket. That's prevent anyone  outside the host preventing accessing the docker daemon 

The first level of security that must think about is securing the daocker host itself from unwanted access.
usual security best practices:
* Controlling root user
* Disabling unused ports
* Disabled password based authentication
* Enable SSH key based authentication
* Determin users who needs acess to the server

If your host has a public facing interface

we also discussed about configuring external access to the docker daemon by enabling the TCP socket. <br>
`$ dockerd --host tcp://192.168.0.1:2375` <br>
`$ export DOCKER_HOST="tcp://192.168.0.1:2375"` <br>

at some time we may really have to allow access to the docker daemon from the another management host. say a user laptop. it need when it absolulately nessecary. <br>

`/etc/var/docker/daemon.json` <br>
`{
    "hosts": [tcp://192.168.0.1:2375]

}` <br>

Now, enables access to the docker daemon from outside the docker host through an interface on our host.<br>
`$ systemctl restart docker` <br>

now, If you have to do this make sure you have exposed the docker daemon on interface, that is private and only accessible from within your organization. <br>
If your host have a public facing interface, make sure the daemon is not exposed on those interface <br>

by allowing external access, we must also secure the communication with TLS Cerficate <br>
so for this we can configure certificate authority (`cacert.pem`), server certificate (`server.pem`) and server key (`server-key.pem`) and we place this on the docker host and configure the `daemon.json` file<br>

`$ dockerd --tlsverify --tlscacert=ca.pem --tlscert=server-cert.pem --tlskey=server-key

**TLS Encryption:** <br>
`/etc/var/docker/daemon.json` <br>
`{
    "hosts": [tcp://192.168.0.1:**2376**] **its important to change 2375 to 2376**
    "tls": true,
    "tlscacert": "/var/docker/tls/server.pem",
    "tlscert": "/var/docker/tls/server-key.pem",

}` <br>

With this anyone outside the docker host can access the docker daemon only if they have the client certificate and key and can access the API and target it docker commands by simply setting the docker host environment variable to point to this host <br>

![TLS Encryption](./images/security/tls-encryption.png) <br>

`$ export DOCKER_TLS=true` // enable secure connection
`$ export DOCKER_HOST="tcp://192.168.0.1:2376" ` <br>
`$ docker ps` <br>


But there still no authentication mechanism in place. meaning that anyone will knows that the docker daemon is being exposed on port 2376 on this host can still access docker daemon by simply setting docker daemon TLS environment variable to true and pointing the docker host environment variable to our host. and they can start deploying ocontainer on our host or delete existing container <br>


Next step is to enable certificate based Authentication: for this we copy the `cacert.pem` to the docker daemon server side and configure `tlscacert` parameter and `tlsverify` in the `daemon.json` file to true.

**TLS Authentication:** <br>
`/etc/var/docker/daemon.json` <br>
`{
    "hosts": [tcp://192.168.0.1:2376"],
    "tls": true,
    "tlscacert": "/var/docker/tls/ca.pem", // to use verify the client certificate
    "tlscert": "/var/docker/tls/server-cert.pem",
    "tlskey": "/var/docker/tls/server-key.pem",
    "tlsverify": true //enables the client certificate authentication
}` <br>

`$ systemctl restart docker` <br>

![TLS Authenticationh](./images/security/tls-auth.png) <br>

So, we genenrate certificate for our client call `client.pem` `clientkey.pem` ensures that securely with the Client server that wants to connect to the host along with the cacert.pem- the certificate of the CA. 

![TLS Authenticationh](./images/security/tls-auth-2.png) <br>

on the client side we set the docker tls verify to true adn then we either passing client certificate to the command line parameter or we drop the certificate into to the `~/.docker` directory under the /user/home directory, from there the docker command automatically pick-up this  certificate. and now only clients with sign certificate from CA server can access the docker daemon. <br>
![TLS Authenticationh](./images/security/tls-auth-3.png) <br>

So remember the TLS option `"tls": true,` alone does not authenticate the client. it only encrypts the communication between the client and the server. <br>
`"tlsverify" :` option is what enabled the client authentication. <br>

#### Summary:

![TLS Authenticationh](./images/security/tls-summary.png) <br>

## Namespaces:
There is no hard isolation between the containers and the underlying host. <br>

Namespace is a feature of the Linux kernel that provides process isolation. It allows multiple processes to run on the same host without interfering with each other. <br>
Docker containers use namespaces to provide process isolation. Each container runs in its own namespace, which isolates it from other containers and the host system. <br>
Namespaces provide the following types of isolation: <br>
1. **PID Namespace**: Each container has its own PID namespace, which isolates the container's processes from the host system and other containers. This allows each container to have its own process tree, with its own init process and PID 1. <br>
2. **Network Namespace**: Each container has its own network namespace, which isolates the container's network interfaces, routing tables, and firewall rules from the host system and other containers. This allows each container to have its own network stack, with its own IP addresses and network configuration. <br>
3. **Mount Namespace**: Each container has its own mount namespace, which isolates the container's filesystem from the host system and other containers. This allows each container to have its own filesystem tree, with its own root directory and mount points. <br>
4. **UTS Namespace**: Each container has its own UTS namespace, which isolates the container's hostname and domain name from the host system and other containers. This allows each container to have its own hostname and domain name. <br>
5. **IPC Namespace**: Each container has its own IPC namespace, which isolates the container's inter-process communication (IPC) mechanisms from the host system and other containers. This allows each container to have its own shared memory segments, message queues, and semaphores. <br>
6. **User Namespace**: Each container has its own user namespace, which isolates the container's user and group IDs from the host system and other containers. This allows each container to have its own set of user and group IDs, which are mapped to different IDs on the host system. <br>
7. **Cgroup Namespace**: Each container has its own cgroup namespace, which isolates the container's control groups (cgroups) from the host system and other containers. This allows each container to have its own cgroup hierarchy, with its own resource limits and accounting. <br>
8. **Time Namespace**: Each container has its own time namespace, which isolates the container's timekeeping from the host system and other containers. This allows each container to have its own clock source and time zone. <br>

CGroups: Control Groups (cgroups) is a feature of the Linux kernel that allows you to limit and monitor the resource usage of a group of processes. Cgroups provide a way to control the CPU, memory, disk I/O, and network bandwidth usage of processes. <br>

Resource Limits CPU, Memory, Disk I/O, Network Bandwidth. It Restrics the resource consumption by the container. <br>
By default there are no restrictions on the resource usage of a container. <br> if require a container can consume all the resources of the host system. <br>

When the kernel detect that a container is consuming all resources, it will start killing the processes in the container to free up resources. <br>
Its important to understand the impact of the containers on resources available on the host. <br>

Forground Process: 
Background Process: `dockerd &` <br> background process is used to run the docker daemon in the background. <br>

**Linux- CPU Sharing:** <br>
CPU Shares: CPU shares are used to allocate CPU resources to containers. By default, all containers have the same number of CPU shares, which means they have equal access to CPU resources. <br>

CFS (Completely Fair Scheduler): The Completely Fair Scheduler (CFS) is the default process scheduler in the Linux kernel. It provides fair CPU scheduling for all processes running on the system. <br>

Real-time Scheduling: Real-time scheduling is a feature of the Linux kernel that allows processes to have guaranteed access to CPU resources. Real-time processes have higher priority than normal processes and are scheduled before them. <br>