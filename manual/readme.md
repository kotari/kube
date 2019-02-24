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


View in a dashboard


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


Namespaces


k get ns
k get po --namespace kube-system
kind: Namespace # if creating with yml file
k create namespace dev
#Deploying into namespace
k create -f {path to yml file} -n {name space}
# pods can talk to other pods in a different namespace - have to look into inter-namespace network isolation


Delete pods


k delete po {pod name}  # deletion based on name
k delete po {pod1} {pod2}
k delete po -l {label key}={label value}
k delete ns {custom namespace} # will also delete the pods under namespace
k delete po {pod name} -n {namespace}
k delete po --all  -n {namespace}   # Deletes all the pods in the namespace
k delete ns {namespace}   # Delete the namespace along with all the pods in the namespace


# Force delete
k delete all --all