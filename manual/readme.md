# Basic Commands


kubectl cluster-info

kubectl get nodes

kubectl describe node {node-name}


# Running image without yaml

kubectl run kubia --image=rkotari/kubia --port=8080 --generator=run/v1  # This creates a ReplicationController behind the scenes

kubectl expose rc kubia --type=LoadBalancer --name kubia-http    #rc - ReplicationController

kubectl expose rs kubia --type=LoadBalancer --name kubia-http    #rs - ReplicaSet

kubectl get services

kubectl get svc

kubectl get pods

kubectl get po

minikube svc kubia-http


# Replication Controller

kubectl get replicationcontrollers

kubectl scale rc kubia --replicas=3

kubectl get pods -o wide  # Will display additional details about the nodes the pods are running on 


# View in a dashboard

minikube dashboard & # push it into background

ps -ef | grep minikube

kubectl create -f {path to yml or json file}

kubectl get po {pod name} -o yaml

kubectl get po {pod name} -o json

kubectl logs {pod name}

kubectl port-forward kubia-manual 8888:8080

kubectl get po --show-labels  # shows all labels

k get po -L {comma separated label names}  # Upper Case L shows all the pods

k label po {pod name} {label key}={label value} --overwrite  # modify an existing one

k label po {pod name} {label key}={label value}  # create a new label


# selecting based on labels need to use lower case l for selection
k get po -l {label key}

# negation
k get po -l '{!label key}'

# Even nodes can be labeled
k label node {node name} ssd=false


# Namespaces

k get ns

k get po --namespace kube-system

kind: Namespace # if creating with yml file

k create namespace dev

#Deploying into namespace
k create -f {path to yml file} -n {name space}

# pods can talk to other pods in a different namespace - have to look into inter-namespace network isolation

# Delete pods

k delete po {pod name}  # deletion based on name

k delete po {pod1} {pod2}

k delete po -l {label key}={label value}

k delete ns {custom namespace} # will also delete the pods under namespace

k delete po {pod name} -n {namespace}

k delete po --all  -n {namespace}   # Deletes all the pods in the namespace

k delete ns {namespace}   # Delete the namespace along with all the pods in the namespace

k delete svc {svcName}

k delete ing {ingressName} # ing is abbrevation for ingress


# Force delete
k delete all --all

# Probes liveness and readiness probe
# if liveness proble bring back a new pod, previous pods logs can be inspected with 
kubectl logs {mypod} --previous

# Set initialDelaySeconds so pods are not restarted when they are coming up

kubectl edit rc {replicationController Name}

kubectl scale rc {replicationController Name} --replicas=10

# Even kubectl edit rc can be used to update the number of replicas
kubectl delete rc {replicationController Name} --cascade=false  #false does not delete the pods, changes will not be cascaded

# DaemonSet, unlike replicationController or replicationSet run a pod for a node.  They can also be configured to run only on nodes that meet a criteria


# Connecting to other pods internally -- is needed to break the commands from kubectl
k exec {mypod} -- curl -s http://svc_ip

k exec -it {mypod} bash --This will put in the interactive terminal just like docker

minikube service {serviceName} --This is confusion still

k get po --all-namespaces

minikube addons list

# To apply contents of the modified yml file
k apply -f {path to updated yml file}

kubectl run dnsutils --image=tutum/dnsutils --generator=run-pod/v1 --command -- sleep infinity

k exec dnsutils nslookup {serviceName}

k get endpoints

# get environment varibales for a pod
k exec {podName} env