---
layout: post
title: "Intro to Docker"
tags:
 -
---

<div class="alert alert-warning text-right pb-0" role="alert">
  <blockquote class="blockquote">
    <p>It works on my system</p>
  </blockquote>
  <figcaption class="blockquote-footer">
     <cite title="Source Title">Every Developer</cite>
  </figcaption>
</div>

For long time, Dev team used to blame operation team and vice-versa for any failure in App deployment. This pressed 
toward the need of isolated environment. The VMs solved the issue but creating a VM is very resource intensive and we have to
install both Operation system and libraries. Then came the concept of Container which provided isolated environment but you dont 
need to install Operating system for every isolated environment.
<img src="https://www.docker.com/sites/default/files/d8/2018-11/docker-containerized-and-vm-transparent-bg.png">


---
Linux for long has concept of `cgroup` and `kernal namespaces`. Docker made these feature approachable. Docker
Container(Running Docker Image) uses isolated file-system.  This custom filesystem is provided by a container image.

The image contains all dependencies,configuration, script and binaries.


<h3 class="alert-success"> Dockerfile:</h3> A text file containing set of instruction to create Container image

<h3 class="alert-success">Container Volume:</h3>
Every Container gets something as scratch space, which is used to File Operation. These changes get lost when container is 
removed. Volumes provide the ability to connect specific filesystem paths of the container back to the host machine. 
There are tow type of Volumes:
1. Names Volumes
2. Anonymous Volumes(Bind Mounts)

```bash
docker volume create todo-db
docker volume inspect todo-db
```

<h3 class="alert-success">Multi-Container Apps</h3>
Each container should do one thing and do it well. Running multiple process will require process manager, which adds 
to complexity. Also, Ideally we will scale our apps separately and may need container manager or container orchestrator
like kubernetes or swarm.
Hence it is ideal to run separate app in other container. Container Networking is used to connect these container as 
container runs in isolation

<h3 class="alert-success">Docker Compose</h3>
A utility tool to setup and teardown multi-container app. With Compose, we create a YAML file(docker-compose.yml) 
to define the services and with a single command, can spin everything up or tear it all down.