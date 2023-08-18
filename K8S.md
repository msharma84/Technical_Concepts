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

1.	**kubelet**	: an agent that runs on each node, it communicate with the master via API, it main job is that the 		containers are running on pods
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
