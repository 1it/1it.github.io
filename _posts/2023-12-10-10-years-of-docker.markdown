---
layout: post
title: "10 Years of Docker: From Revolutionary Idea to Modern Practice"
date: 2023-12-10
categories: [containers, devops]
tags: [docker, containerization, infrastructure, history]
---

Nowadays, virtualization has become a fundamental technology for optimizing server performance and simplifying application development and deployment processes. However, until the advent of Docker, the application build and deployment process remained a relatively complex and slow process. Honestly speaking, it still could be a very slow process, but that’s a different story.

Over the past 10 years, Docker has revolutionized the world of virtualization and become an indispensable tool for DevOps practitioners. During this time, containerization has become so widespread and familiar to so many people that they don’t even think about how it works under the hood. From my interviewing experience, the question “What is Docker?” often confuses people. I think it’s quite important to deeply comprehend things. That way, it helps effectively solve problems and understand at which layer of the system something may go wrong.

In this article, I will share a brief overview of the history of Docker, its key concepts, and misconceptions. I hope this will be useful for beginners and students learning DevOps practices and virtualization.

## The emergence of Docker

Before Docker was born, there were other containerization technologies such as LXC (Linux Containers) and OpenVZ.There were also projects for isolating processes at the file system level like jails and chroot, but that’s a completely different story. These projects also provided tools for creating isolated environments, but they did not have the same degree of simplicity and portability as Docker.

Docker took inspiration from these early technologies and leveraged LXC as one of its first container management engines. However, Docker added a layer of abstraction and simplified the process of creating and managing containers, making it more accessible to a wider audience of developers and system administrators.

Thus, Docker not only improved the concept of containerization but also made it more accessible and widely applicable. This combination of usability and efficiency has over time made Docker the dominant technology in the world of containerization and DevOps.

The fact is that developers and administrators have always faced several difficult tasks in creating, monitoring the consistency of environments, and scaling services. Traditional virtual machines require large resources and time to start. Managing applications and their dependencies has been and still is a non-trivial task.

Docker appeared as a response to the challenges of that time, from people who knew firsthand all the pain and problems of the industry. This project was launched by dotCloud and its founder Solomon Hikes in 2013 and quickly became an effective solution for application containerization. But it wasn’t always like this and, of course, it didn’t happen right away.
Tweet by Solomon Hikes

Before the first public release, the Docker prototype was a set of shell scripts. Later, the project switched from Python to Golang, at the same time contributing to the popularization of the young programming language.
Sebastian van Steyn (Runtime lead, Staff Software Engineer, Docker) and Frederick Kautz (former Docker team engineer) about the history of Docker creation.

Docker solved many problems thanks to the following features:

- Isolation: Docker allows you to run applications in isolated containers, which provides a level of isolation comparable to virtual machines, but with much less overhead.
- Portability: Docker containers can be run on any platform where Docker is installed. This makes application development and deployment more convenient and predictable.
- Dependency management: Docker allows you to package an application and its dependencies into a single container, providing reliable dependency and version control.

## Adoption of Docker by the community

Immediately after its release, Docker quickly gained popularity among developers and system administrators. The community has followed the project closely, creating many tools and solutions based on Docker.

It is worth noting that Docker emerged at a time when virtualization technologies like Xen, KVM, and VMWare were the standard, and the creation and control of VMs for running services and development environments were managed by orchestration tools like Puppet, Chef, and many others. This has been the industry standard for quite a long time.

There were a lot of certified specialists of different stripes on the market, and not all of them — including the author of the article — immediately understood and accepted the new tool. Perhaps this has given rise to many misconceptions about the use of containerization and led to undeserved criticism.

Many developers and administrators used Docker for other purposes, considering it as a more convenient and lightweight replacement for VMs. Treating Docker, containers as a full-fledged OS, people were running multiple processes in them, which was doable but not an intended use for a single-process environment.

For example, I witnessed how people launched their PHP application, an SSH daemon, and, for example, a Zabbix or Nagios agent using a supervisor (at that time things like Zabbix, Nagios and its forks were very popular).

Despite its impressive success and attention from the community, Docker also faced constructive criticism during the initial stages of its development. Comments were most often directed at the following aspects:

- Process isolation: Docker does not provide the same degree of isolation as traditional virtual machines. This means that containers can influence each other, which raises security and stability concerns.
- Network configuration complexity: Setting up networking for containers in Docker can be challenging, especially when working with multiple containers and microservice architectures.
- Monolithic application: In the early days, Docker containers were sometimes used to run monolithic applications, which was not always the best practice for microservice architectures.

It’s worth noting that the Docker community has been actively working to improve and resolve these issues. Subsequent versions of Docker introduced many improvements in security, isolation, and network management. Criticism became the driving force behind the development of Docker, and it has improved greatly over time.

There was also a strange moment in history when one day, without a notice and a proper explanation, Docker was renamed to Moby. This caused everyone to be at least bewildered. The change of name on GitHub and, accordingly, the change of all paths in the code was not very warmly received by the community and especially by the project’s contributors. From this point on, the commercial company Docker began to actively look for ways to make money on its product without abandoning its Open Source roots.

## What Docker really is

Docker is a tool that is used to automate the deployment of applications in lightweight containers so that applications can effectively run in different environments in isolation.

Docker consists of several key components:

- Docker Engine: Docker core (daemon) that manages containers;
- Docker Containers: isolated environments in which applications run;
- Docker Images: templates for creating containers;
- Docker Registry: a repository for storing and sharing Docker Images;
- Docker CLI: console utility for interacting with the above components.

A large ecosystem of tools and products has developed around Docker. The Docker Hub service became so popular among developers that at some point Docker had to introduce limits on downloading public images — the total monthly number of downloads has long exceeded 10 billion.

Docker Desktop makes it possible to run and use Docker components on non-Linux systems with almost the same convenience as in a native environment. It allows developers and administrators to quickly deploy any services, build, and test consistently, regardless of their operating OS: MacOS or Windows.

Also, for example, Docker Compose allows you to define and run multiple containers simultaneously, incl. and on multiple hosts using Docker Swarm. Kubernetes (which not long ago deprecated the Docker Engine container runtime in favour of Containerd) provides orchestration of containers in large and small (hello Minikube!) clusters.

## Kernel technologies used by Docker

In addition to Golang, which, together with the community, made a significant contribution to the success of the project, Docker stands on the powerful shoulders of Linux. It relies on a number of key technologies from the Linux operating system kernel to provide isolation and container management:

- Namespaces: Linux kernel technology developed back in 2002. Docker uses namespaces such as PID (Process ID), Network, and Mount to create isolated namespaces. For example, using PID namespaces, each container can access only its own processes, which provides process isolation between containers.
- Cgroups (Control Groups): a technology developed internally by Google engineers back in 2006. Control groups are used by Docker to limit the resources available to a container: CPU, memory, and disk space. This helps prevent resource starvation and ensures fair distribution of system capacity between containers.
- Union File Systems: Docker uses “layered” file systems such as AUFS, OverlayFS, and Overlay2 to create lightweight and efficient container images. These layers allow sharing of common files among containers (using the same images), saving disk space.
- Seccomp (Secure Computing Mode): Docker can use Seccomp to improve security. It limits the container’s access to system calls, which reduces the attack surface and prevents dangerous operations from being performed.
- Capabilities: The Linux kernel provides various capabilities to perform privileged actions. Docker allows you to customize the set of capabilities available to the container to fine-tune security. For example, dropping “cap_net_bind_service” will disallow the container to use network ports from a range below 1024, like the default HTTP/HTTPS ports — 80/443.

All these technologies allow Docker to create isolated and lightweight containers running on the shared operating system kernel but with a high level of isolation from each other. Docker provides an environment in which applications can run independently of each other while ensuring efficient use of resources and simplifying container management.

## How to use Docker correctly

For maximum efficiency and security when using Docker, follow these practices:

- Isolate dependencies: Each container should contain only the necessary dependencies to run the application. Use a multistage build, do not leave temporary files or packages in the image.
- Follow the One Process Principle: Each container should only run one process. This makes it easier to track and manage containers.
- Update images regularly: Update your images regularly to get the latest security updates and bug fixes.
- Practice monitoring and logging: Use monitoring and logging tools to track container performance and identify problems.
- Don’t forget about security: Don’t ignore basic security principles such as limiting host access and controlling access to resources.
- Don’t run containers with privileged rights: avoid using flag — privileged, which gives the container full (privileged/root) access to the host.
- Don’t store sensitive data in images: Do not include secret keys or passwords in Docker images. Use secret storage mechanisms such as Vault or Docker Secrets.

## Why Docker is a revolution

Docker has changed the virtualization landscape and has become an indispensable tool for DevOps practitioners. Its ease of use, efficiency, and broad ecosystem make it the first choice for application containerization. Unifying the processes for building and delivering code had a significant impact on the industry as a whole, ultimately saving a huge amount of both man-hours and machine (computing) time and, as a result, money.

The emergence and popularization of Docker gave impetus to the creation of many new technologies, such as rkt, Podman, Kubernetes, kind, Rancher, and Dokku. Many new services have also appeared: starting from public Container Registry from quay.io to gcr.io, ending with Serverless services — ECS, Cloud Run, and so on.

After 10 years, Docker’s enormous contribution to the development of the industry is difficult to overestimate, and it is even more difficult to say what this impulse will bring us in the future. Only one thing can be said with confidence: “The revolution has happened!”

## Resources
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Container Security Best Practices](https://docs.docker.com/develop/security-best-practices/)
