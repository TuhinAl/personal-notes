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






Forground Process: 
Background Process: `dockerd &` <br> background process is used to run the docker daemon in the background. <br>