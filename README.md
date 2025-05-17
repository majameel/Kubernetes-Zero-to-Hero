# Kubernetes-k8s
All About Kubernetes 

# Pre-requisites to learn Docker 
While "Docker" is often used because people are more familiar with the term, the core requirement is understanding the concept of containers. This means understanding:

- What containers bring into the picture
- How they are different from virtual machines
- Networking isolation
- Namespace isolation
- Why containers are lightweight
- How to secure containers (using distroless images, multi-stage Docker builds)

You should be strong with the basics of containers, not just simple Docker commands. It is assumed you have watched the previous videos or already understand these concepts before proceeding with Kubernetes.

## Key question - Docker vs Kubernetes 

The fundamental question before learning Kubernetes is:

**What is the difference between Docker and Kubernetes?**

- **Docker** is described as a **container platform**. It makes interacting with containers and their life cycle easy, providing tools like the Docker engine and Docker CLI.
- **Kubernetes** is a **container orchestration platform**. This is the textbook definition.

![image](https://github.com/user-attachments/assets/fb0dcec2-4090-4339-9758-273ebd094553)


## Limitations of Docker (Problems It Doesn't Solve)

To understand the practical difference, we need to look at the problems with using just Docker or a simple container platform. The video outlines **four key problems**:

### 1. Problem 1: Single Host Scope

- Docker is typically installed on a single host, like a personal laptop or an EC2 instance.
- If you have multiple containers running on this single host (e.g., 100 containers), they can impact each other, especially regarding resources.
- Example: If one container starts consuming a lot of memory, it can affect other containers on the same host.
- Due to how Linux works with process priorities, the kernel might decide to kill another container that isn't getting enough resources.
- This problem arises because the Docker platform is limited to the scope of one single host.

### 2. Problem 2: Lack of Auto Healing

- Containers are **ephemeral**, meaning they are short-lived or short-living. They can die or revive anytime.
- If a container dies, the application running inside it becomes inaccessible.
- In Docker, if a container is killed (whether intentionally or due to an issue), it does not automatically restart. Someone (a user or devops engineer) has to manually start the container again.
- This is problematic in production environments where you might have thousands or millions of containers.
- A devops engineer cannot constantly monitor all of them manually using commands like `docker ps`.
- **Auto healing** is the desired behavior where a container starts by itself without manual intervention if it goes down. Docker lacks this important feature.

### 3. Problem 3: Lack of Auto Scaling (and Load Balancing Integration)

- Applications experience fluctuating user load, especially during events like festivals or popular movie releases (using the Netflix example).
- The load can increase dramatically (e.g., from 10,000 users to 1 lakh or 1 million).
- To handle increased load, you need to scale the application, usually by increasing the number of container instances.
- In Docker, this doesn't happen automatically. You would have to manually create more instances of the container.
- Furthermore, if you have multiple container instances serving the same application, you need a **load balancer** to distribute incoming user requests.
- End users expect to access a single URL (like netflix.com) without needing to know about individual container addresses.
- Docker by itself does not support automatic scaling or the integrated load balancing mechanism needed to effectively handle increased traffic across multiple container instances.

### 4. Problem 4: Lack of Enterprise Level Support

- Docker is described as a very minimalistic or simple platform.
- By default, Docker does not provide support for many features required for running enterprise-level applications in production.
- Examples of missing enterprise features include built-in support for:
    - Load balancers
    - Firewalls
    - API gateways
    - Auto scaling
    - Auto healing
    - Whitelisting
    - Blacklisting
- While you might use Docker Swarm in production, Docker *independently* is generally not used because it's not a complete enterprise solution.
- Organizations running critical applications require capabilities like blacklisting malicious IPs or protecting against DDOS attacks, which basic Docker doesn't provide out-of-the-box.

![image](https://github.com/user-attachments/assets/7e60039e-398c-4c9b-8b91-f2f6ebec87bb)

## Kubernetes: The Solution

So, **who is solving all of these problems?**

The simple answer is: **Kubernetes**.

---

## How Kubernetes Solves These Problems

### Solves Problem 1 (Single Host): Kubernetes is a Cluster

- By default, Kubernetes is a **cluster**, which is a group of nodes.
- While you can install it on a single node for development, in production, it's installed as a master node architecture with multiple nodes.
- Because it has multiple nodes, if a container (or rather, a **pod** in Kubernetes terminology) on one node is impacted, Kubernetes can **move that pod to a different node** in the cluster.

### Solves Problem 2 (Lack of Auto Healing): Auto Healing Feature

- Kubernetes has an **Auto healing feature**.
- It continuously monitors the state of applications.
- If Kubernetes detects that a container/pod is going down (or even before it fully fails), it will **automatically start a new container/pod**.
- This self-healing behavior ensures the application remains available to the end user without requiring manual intervention.

### Solves Problem 3 (Lack of Auto Scaling): Replica Sets, HPA & Load Balancing

- Kubernetes uses **Replica Sets** or **Deployment objects** to manage multiple instances.
- Scaling can be done **manually** by changing the replica count in a YAML configuration file.
- Kubernetes supports **Horizontal Pod Auto Scaling (HPA)** to increase pods based on metrics like CPU usage.
- Built-in load balancing through **Services** and **Kube-proxy** provides basic round robin mechanisms.
- Kubernetes also supports **Ingress Controllers** (e.g., Nginx, Traefik) with **Custom Resources (CR)** and **Custom Resource Definitions (CRD)** for advanced load balancing.

### Solves Problem 4 (Lack of Enterprise Support): Enterprise-Grade Platform

- Kubernetes was developed by **Google** (based on their internal Borg system) as an **enterprise-grade container orchestration platform**.
- Provides out-of-the-box support for:
    - Load balancers
    - Firewalls
    - API gateways
    - Auto scaling and healing
    - Whitelisting and blacklisting
- Backed by the **CNCF (Cloud Native Computing Foundation)** with strong community support.
- Kubernetes is **extensible** through **CR and CRD**, making it suitable for integration with third-party tools and advanced custom features.

![image](https://github.com/user-attachments/assets/ba0f0555-c8c2-4f2d-a20f-4e72fcd9994a)

## Summary

- Kubernetes was built to address the fundamental limitations of Docker in complex, large-scale, and critical production environments.
- The speaker reiterates that **Kubernetes is easy**—if you understand **why** you need it.
- Understanding the problems it solves (the first 5%) builds the foundation for learning the rest (the next 95%).
![image](https://github.com/user-attachments/assets/3f7af56f-9879-4249-ab19-c29f356a0a6c)


