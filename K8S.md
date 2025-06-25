# Kubernetes (k8s)
Kubernetes (k8s) is an open-source system for automating deployment, scaling and management of containerized application.
It groups containers that make up an application into logical units for easy management and discovery.

It was originated in Google, in 2015 google release Kubernetes as an open source project, shortly after it was donated to CNCF for promoting container technology

Various advantages of k8s: 

1. 	Automates various manual process.
2. 	Interacts with several groups of containers
3. 	Self-healing and Self-monitoring
4. 	Horizontal Scaling
5. 	Storge Orchestration
6. 	Automates rollouts and rollbacks
7. 	Container load balancing
8. 	Run everywhere / supports On-prem / Cloud / Hybrid environment
9. 	Fast paced deployment techniques
10. Declarative configuration
11. Decoupling / Supports micro-services ecosystem / seperation of concerns
12.	Provides efficiency - both cost efficiency and operational efficiency
13. Portability / Modularity
14. Provides additional capabilities

Disadvantage of k8s:

1.	Some degree of complexity of setup
2.	Network latency and limitations

## What is a cluster?

A cluster consists of at least one master cluster and multiple worker machines called nodes. When the programs or applications are deployed onto a cluster, it intelligently handles distributing work to the individual nodes via master. A cluster is a "master-nodes" architecture.

Master components are also know as Decision Makers, it's consists of :

1. **kube-apiserver**: it process / validated the json or yaml file that contains the information such as name, 		label and specification about the entity
2. **kube-scheduler** : this is the head of all the scheduling task, if any pods are unavailable then this component 	will ensure it avaialable at another pod
3. **kube-controller-manager** : a controller watches the state of the cluster through kube-apiserver and makes 		changes to get the desired state. It's a continuously watching deamon process which manages all the system 		example - Node Controller, Replication Controller, Endpoints Controller etc.
4. **etcd** : Storage for the k8s cluster ( Key Value pair format), only kube-apiserver will be able to communicate 	with etcd

Node components it's consists of :

1.	**kubelet**	: an agent that runs on each node, it communicate with the master via API, it main job is that the containers are running on pods
2.	**Container Runtime** : responsible for downloading and running the containers
3.	**kube-proxy** : maintains the network rules on the host

## What is a Pod?

Single instance of an application in k8s, which consists of either a single container or a small number of containers
that are tightly coupled and share resources. It runs on a single node and represents a unit of deployment in k8s.

1. Pods are atomic, building blocks of k8s.
2. A Pod can only run on a single node at a given time
3. Pod is the unit of scaling in k8s
4. Each Pod is assigned a unique IP address. Containers inside a Pod can communicate with one another using localhost
5. All containers in the Pod can access the shared volumes, allowing those container to share data

## What is a namespace?

A way of grouping the pods for variety of purposes, can be used for providing the quotas and limits around resource usage have an impact on DNS name that k8s create internal to the cluster and in the future may impact access control policies. Namespaces could also be used to divide the cluster resources between various users.

Command to view all namespaces: 
```kubectl get pods --all-namespaces```

k8s starts with three intial namespaces:
1. default
2. kube-system - for the object created by the kubernetes system
3. kube-public - created automatically and is visible and readable by all the users throughout the whole cluster

## What is a Label?

Tag that can be attached to kubernetes object to mark them as a part of a group. An object can have multiple labels, but the keys must be unique.

## What is an Annotation?

Allows you to attach key-value information as metadata to an object.

## What is a Replication Controller?

It ensures that a specified number of pods replicas are running at any one time. It starts or terminates the pods depending on the desired state. Pods maintained by replication controller are automatically replaces if they are fail, are deleted, or terminated.

1. RC starts/stops pod depending on the desired state
2. Error correction and detection
3. Ease of supervision and management
4. Supervises multiple pods across multiple nodes

## What is a Replica Set?

Created using deployment, this is a declarative way of ensuring that a specified number of pod replica are running at any given time. It starts or terminates the pods depending on the desired state. It allows access to pods within each other inside a cluster as well as outside of it.

## What is a Service?

An abstraction which defines a logical set of Pods and a policy by which to access those pods. It facilitates access to the pods within the cluster or outside of it. 

### Types of Services: 
#### Cluster IP
* With this type (default) the service can be reached only from within the cluster
* Assign the service it's own IP address

#### Node Port
* This option is used if the service is to be accessed from outside the cluster. It exposes the service on each Node's IP at a static port (the NodePort). So the service accessed using the **<NodeIP>:<NodePort>**
* If the type field is NodePort, the kubernetes master will allocate a port of the range specified by the **--service-node-port-range** flag (default: 30000-32767), and each Node will proxy that port ( the same number on every Node) into the service
* Specific port number can be used in the NodePort field, and the system will allocate that port.

#### Load Balancer
* Exposes the service externally using a cloud provider's load balancer(Ex- Elastic Cloud Load Balancer of AWS).
* Provides ExternalIP to access the service
  
#### External Name
* Simply provide a DNS reference called as ExternalName
* Does not include a selector, and doesn't include any port references either. Instead, it simply defines and external DNS entry that can be used as a service definition.

## What is Service Discovery?

It's a process for finding out how to connect to a service. It can discovered by
* Environment Variables
* Using Domain Name System

## What is Deployment?

A Deployment controller provides declaritive update for Pods and ReplicaSets. Once the desired state is described in the Deployment object, and the Deployment controller changes the actual state to the desired state at a controlled rate.

## What is a Volume?

A storage that is accessible to the containers in a Pod. A pod can specify a set of shared storage volumes.

## What is a Container Probes?

A Probe is a diagnostic performed periodically by the kubelet on a container. This helps k8s identify what is going on the pods and their containers. There are two types of container probes:
1. **livelinessProbe**	:	Indicates whether the container running
2. **readinessProbe**	:	Indicate whether the container is ready to serve the request

   
