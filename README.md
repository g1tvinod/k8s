# k8s

```
$ kubectl get nodes
NAME             STATUS   ROLES           AGE   VERSION
docker-desktop   Ready    control-plane   31d   v1.25.9

$ kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
deployment.apps/kubernetes-bootcamp created

$ kubectl get deployment
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
guestbook-ui          1/1     1            1           11d
kubernetes-bootcamp   1/1     1            1           119s
my-api                1/1     1            1           28d

$ kubectl get pods
NAME                                   READY   STATUS    RESTARTS        AGE
guestbook-ui-b848d5d9d-pp58r           1/1     Running   1 (4d21h ago)   11d
kubernetes-bootcamp-75c5d958ff-pw2tk   1/1     Running   0               5m12s
my-api-78798b59d4-6nm2l                1/1     Running   6 (4d21h ago)   28d

$ kubectl logs kubernetes-bootcamp-75c5d958ff-pw2tk
Kubernetes Bootcamp App Started At: 2023-07-08T03:23:59.160Z | Running On:  kubernetes-bootcamp-75c5d958ff-pw2tk

$ kubectl exec -ti kubernetes-bootcamp-75c5d958ff-pw2tk -- bash

$ kubectl get services
NAME             TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
kubernetes       ClusterIP   10.96.0.1      <none>        443/TCP   31d

$ kubectl expose deployment/kubernetes-bootcamp --type="NodePort" --port 8080
service/kubernetes-bootcamp exposed

$ kubectl get services
NAME                  TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)          AGE
kubernetes            ClusterIP   10.96.0.1      <none>        443/TCP          31d
kubernetes-bootcamp   NodePort    10.104.74.3    <none>        8080:30454/TCP   10s

$ kubectl describe services/kubernetes-bootcamp
Name:                     kubernetes-bootcamp
Namespace:                default
Labels:                   app=kubernetes-bootcamp
Annotations:              <none>
Selector:                 app=kubernetes-bootcamp
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.104.74.3
IPs:                      10.104.74.3
LoadBalancer Ingress:     localhost
Port:                     <unset>  8080/TCP
TargetPort:               8080/TCP
NodePort:                 <unset>  30454/TCP
Endpoints:                10.1.0.64:8080
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

$ export NODE_PORT="$(kubectl get services/kubernetes-bootcamp -o go-template='{{(index .spec.ports 0).nodePort}}')"
$ echo "NODE_PORT=$NODE_PORT"
NODE_PORT=30454

$ kubectl scale deployments/kubernetes-bootcamp --replicas=2
deployment.apps/kubernetes-bootcamp scaled

$ kubectl get deployment
NAME                  READY   UP-TO-DATE   AVAILABLE   AGE
kubernetes-bootcamp   2/2     2            2           25m

```

![image](https://github.com/g1tvinod/k8s/assets/45305248/cd4194bb-b5ee-41b9-9cca-5c7d744a0709)
