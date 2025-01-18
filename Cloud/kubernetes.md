# What is kubernetes

Kubernetes is a container orchestration tool. That means it helps you manage containers. 

When the industry was moving towards microservices from monolith and also there was rise of the usage of containers. Because of this sometimes companies had many containers and sometimes even hundreds of containers running in production. It was difficult to manage many containers with self made tools, so to avoid this google created Kubernetes, which became a industry standard now to orchestrate and manage container environment for the application in production.

Kubernetes offers:

* High availability
* Scalability
* Disaster recovery

# Kubernetes Architecture

A k8s cluster consists of a control plane plus a set of worker machines, called nodes. Every cluster needs at least one worker node in order to run pods.

## Node

A node maybe a virtual or physical machine that runs the containers and the workload of the kubernetes.

Kubernetes runs your workload (an application running on kubernetes) by placing containers into pods to run on nodes. Typically you have several nodes in a cluster. A node will have all the resources  to run workloads.

The components of the Node are:

1) Kubelet
2) container runtime
3) kube-proxy

Node is identified by name. Two nodes cannot have the same name at the same time.

There are two ways nodes are added to the API server:

1) Self-registration: When the kubelet flag --register-mode is true, kubelet will attempt to register itself with API server.
2) Manually: User will create and modify the node objects using kubectl

### Kubelet

An agent that runs on each node of the cluster. It makes sure that pods are running. In simpler terms, the Kubelet is the "executor" on the node that makes sure your application (represented as Pods) is running and behaving as expected.

The Kubelet is responsible for:

1. Communicating with the **control plane**, especially the **API Server**.
2. Managing container lifecycle on the node.
3. Monitoring and reporting the node's status to the control plane.

`Its main purpose is to make sure that the pods are in desired state`

#### kubelet workflow

1. A user creates a Deployment or Pod through `kubectl`.
2. The API Server updates the desired state in `etcd`.
3. The Scheduler assigns the Pod to a specific node.
4. Kubelet on that node:
    - Receives the PodSpec from the API Server.
    - Pulls the required container images.
    - Creates and starts the containers.
5. Kubelet continuously monitors the running containers and reports their status back to the API Server.

PodSpec - it is yaml or json object that describes a pod. The kubelet takes a set of podSpecs that are provided through various mechanisms and ensures that the containers described in those PodSpecs are running and healthy.

## Container runtime 

Is the component/software responsible for running containers. You need to install a [container runtime](https://kubernetes.io/docs/setup/production-environment/container-runtimes) into each node in the cluster so that Pods can run there.

Some common container runtimes are:

* containerd
* Docker Engine
* Mirantis Container Runtime

#### Docker engine vs containerd

- **containerd** is a lightweight runtime focusing solely on managing container lifecycles, making it ideal for integration with systems like Kubernetes.
- **Docker Engine** is a complete platform built on top of containerd, providing additional tools, CLI, and user-friendly features for developers and admins.

## kube-proxy

It is a network proxy. This adds network rules on nodes. These network rules allow network communication to your pods from inside or outside your cluster.

## Control plane

Its known as master node which controls the worker nodes. The control plane's component makes global decisions about cluster (like scheduling) as well as detecting and responding to cluster events.

Control plane can run on any machine in the cluster. However, its a good idea to have a separate machine for it and not run nodes on this machine. Since, this is the most important component we should have backup for it by have a standby control plane.

### Kube-api server

*Entry point to k8s cluster*

All the external resources like UI, API or CLI will interact with API Server. This is the component in control plane which send PodSpec to the kubelet.

It is a component of control plane that exposes the k8s API. It is like a frontend for the k8 control plane.

### Control manager

*Keeps track of what is happening in the cluster*

It is basically a controller are control loop. A control loop is a non terminating loop that regulates the state of the system.

In Kubernetes, controllers are control loops that watch the state of your [cluster](https://kubernetes.io/docs/reference/glossary/?all=true#term-cluster), then make or request changes where needed. Each controller tries to move the current cluster state closer to the desired state.

There are different types of controllers. like:
* Node controller - Notice and responds when nodes go down through API server

### Scheduler

*Ensures Pods placement*

Its control plane component that watches for newly created pods with no assigned node and selects a node from them to run on. To places the pod on to correct node based on different factors like resource based on workload and requirements, hardware/software constraints etc.

## Etcd

`Kubernetes backing store`

A highly available key value store that stores the state of the cluster.  It stores all the information and all the state of the cluster here. This is helpful for backup and store strategy. We can backup whole cluster and bring it up using etcd


# Kubernetes components

## Pod

`A good way to see a pod as an extra layer over a container.`

They are the smallest unit of k8s. _It is a abstraction over container_. You application is finally running in a pod. You can run multiple applications in a pod but ideally it is a good practice to run just 1 application per pod.

Each pod has its own internal ip-address assigned to it. Pods are ephemeral like docker containers, this means when a pod goes down or deleted the ip address and also the data in it will be deleted and when it comes up kubernetes assigns it a new ip address. To avoid changing our code when a new ip address is changes to be able to always communicate with a pod we should use a service.

## Service and ingress

Service is a static IP address that can be attached to each pod. Lifecycle of pod and service is not connected, so we don't have to rely on the ip address of the pod we can connect to pod using a service.

They enable communication between different components of a Kubernetes cluster and allow external users to access applications running inside the cluster. It also provides load balancing between pods and across nodes.

### Types of Kubernetes Services

1. **ClusterIP (Default)**:
    - Exposes the Service within the cluster only.
    - Accessible via a stable internal IP and DNS name.
    - Use Case: Communication between internal components like microservices.
2. **NodePort**:
    - Exposes the Service on a specific port of each node in the cluster.
    - Accessible externally via `<NodeIP>:<NodePort>`.
    - Use Case: Basic external access for testing purposes.
3. **LoadBalancer**:
    - Creates an external load balancer (e.g., from a cloud provider) to expose the Service to the internet.
    - Use Case: Production environments requiring external access.
4. **ExternalName**:
    - Maps a Service to an external DNS name instead of routing traffic to Pods.
    - Use Case: Accessing external resources like APIs.

## Ingress

Ingress is a kubernetes resource which exposes HTTP and HTTP routes from outside the cluster to services within the cluster. 

You can provide protocol based mechanisms here. It acts as a reverse proxy and can handle advanced traffic routing, SSL termination, and load balancing.

#### How Ingress Works

1. **Ingress Controller**:
    
    - An Ingress resource itself does nothing; it requires an **Ingress Controller** to interpret the rules and manage the actual routing.
    - Examples: NGINX, Traefik, HAProxy.
2. **Rules Definition**:
    
    - An Ingress resource specifies routing rules that map HTTP/HTTPS requests to Services.
3. **External Access**:
    
    - The Ingress Controller listens for traffic on the cluster’s external interface and routes it to the appropriate Service based on Ingress rules.


So now the traffic first goes to Ingress and from there it is forwarded to the internal services inside the cluster.

### How Services and Ingress Work Together

1. **Services for Pod Access**:
    - Each application is exposed internally within the cluster using a Service.
    - Services load-balance traffic across the Pods of the application.
2. **Ingress for External Access**:
    - An Ingress resource is created to route external traffic to the appropriate Services.
    - The Ingress Controller implements the rules defined in the Ingress resource.

## ConfigMap

*External configuration of your application*

A ConfigMap is an API object used to store non-confidential data in key-value pairs. [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) can consume ConfigMaps as environment variables, command-line arguments, or as configuration files in a [volume](https://kubernetes.io/docs/concepts/storage/volumes/).

For the configuration data of the application, you can store it inside the pod in the application, but if there is any change in the configuration then you have to change the application code. Instead of that we can keep the configuration file outside the node and pods and then access it using the environment variables inside the pods. Now to make any configuration changes you have to just make a change in the configMap and pods will get those changes automatically.

Contains configuration data like url of data or other services and in kubernetes you just connect it to pod and application gets all the configuration. So now to make any application configuration changes can be done in this external files.

All passwords, certificates etc can go here. You can even use the secrets from here in the pods using environment variables.

ConfigMap does not provide secrecy or encryption. If the data you want to store are confidential, use a [Secret](https://kubernetes.io/docs/concepts/configuration/secret/) rather than a ConfigMap, or use additional (third party) tools to keep your data private.
## Secrets

*Used to secret data*

A Secret is an object that contains a small amount of sensitive data such as a password, a token, or a key.

Data here is stored in Base 64 encryption. But this does not make it more secure, you should use encryption services provided by cloud services to encrypt the data here. Meaning, you should have encryption at rest implemented to make it secure. 

Secrets are similar to [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/) but are specifically intended to hold confidential data.

## Volumes

Kubernetes _volumes_ provide a way for containers in a [pods](https://kubernetes.io/docs/concepts/workloads/pods/) to access and share data via the filesystem durably storing data so that it stays available even if the Pod restarts or is replaced.

### Persistent volumes

A _PersistentVolume_ (PV) is a piece of storage in the cluster that has been provisioned by an administrator. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual Pod that uses the PV.

A _PersistentVolumeClaim_ (PVC) is a request for storage from a pod by user. It is similar to a Pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory).

So, to make persistent volumes work in a pod, we first need to create a persistent volume, where we give all the information like how much total storage is assigned to the cluster. And once we have this storage ready then every individual pod can use persistent volume claim  to get storage which has information like how much specific storage or type a  pod needs from the PV.

## Deployment

Deployments manage set of pods to run an application workload. Deployment are the resources you use to create pods with workloads. You describe a desired state in a deployment and kubernetes changes the actual state to the desired state at a controlled rate.

To create a deployment you have to use a YAML configuration file, where you mention all the details of the pods. After that you can execute this file using kubectl cli tool

## Statefulset


StatefulSet is the workload API object used to manage stateful applications.

Deployment are generally meant for stateless pods/applications. If you want to maintain the state of the application, like for pod running the database, then you have to use statefulset. This can be tricky and difficult to maintain so its better to keep your cluster stateless and then keep your state outside the cluster like having database outside the cluster. K8s is meant to handle the compute of the application and not storage or state.

Manages the deployment and scaling of a set of [Pods](https://kubernetes.io/docs/concepts/workloads/pods/), _and provides guarantees about the ordering and uniqueness_ of these Pods.