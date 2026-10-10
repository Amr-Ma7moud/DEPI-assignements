create the deployment: `k create deploy --image amrctl/docker-task:0.1 --replicas 3 -o yaml --dry-run=client web-server > web-server.deploy.yaml`

create the ClusterIp svc: ` kubectl expose deployment web-server --name=web-clusterip --type=ClusterIP --port=80 --target-port=8080 -o yaml --dry-run=client > svc.yaml`

create the NodePort svc:
`kubectl expose deployment web-server --name=web-nodeport --type=NodePort --port=80 --target-port=8080 --dry-run=client -o yaml > nodePort-svc.yaml`

create the HPA:
`kubectl autoscale deployment web-server --cpu=70% --min=3 --max=10 -o yaml --dry-run=client > HPA.yaml`

install the metrics server:
`kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`
