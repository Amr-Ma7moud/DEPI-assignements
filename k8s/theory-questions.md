Theory
a)
1.  .
	1. control plane: manage clusters and ensure the desired state of the system
	2. node: run the application pods
	3. etcd: where configurations and state lives
	4. pod: smallest deployable unit i k8s
	5. kube-apiserver: expose k8s APIs and receive requests to manage the resources
	6. kubelet: ensures the containers in pods are running and healthy 
2. 
	Pods: smallest deployable unit in kubernetes that may contain one or more container which share network resources which mean pod is just a wrapper around the container
	container: is an individual containerized application process. Kubernetes schedules and manages Pods rather than scheduling individual containers directly. **Most** Pods contain one application container
b)
	1. A Deployment manages replicated Pods and ensures that the desired number of replicas is maintained. It supports automatic replacement of failed Pods, rolling updates, and rollbacks.
	2. 
		1. clusterIP: Provides an internal cluster address
		2. NodePort: Exposes a Service through a port on each node.
		3. LoadBalancer: Requests an external load balancer from a supported infrastructure provider or from installed one (in case of on-premise deployment)
C)
- Kubernetes can scale applications manually by changing their replica count or automatically using a Horizontal Pod Autoscaler
- HPA periodically monitor the application and check metrics such as average CPU, RAM usage to scale up/down the pods accordingly based on the specified desired state
