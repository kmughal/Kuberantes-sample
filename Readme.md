# Introduction

This is a sample code for kubernates. 

## How to setup ?

- install docker desktop
- install minikube `minikube start --driver docker`
- Follow below instructions:

```
$ kubectl apply -f mongo-config.yml 
configmap/mongo-config created
$ kubectl apply -f mongo-secrets.yml 
secret/mongo-secrets created
$ kubectl apply -f mongo.yml 
deployment.apps/mongo-deployment created
service/mongo-service created
$ kubectl apply -f web.yml 
deployment.apps/web-deployment created
service/web-service created
$ kubectl get pod
NAME                                READY   STATUS    RESTARTS   AGE
mongo-deployment-5fcf84768f-s8pz9   1/1     Running   0          15s
web-deployment-fcc87bb9f-m6c8p      1/1     Running   0          4s
$ kubectl get svc
NAME            TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE
kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP           2m10s
mongo-service   NodePort    10.105.77.118   <none>        27017:30100/TCP   97s
web-service     NodePort    10.110.32.249   <none>        3000:30200/TCP    86s
$ kubectl get secrets
NAME            TYPE     DATA   AGE
mongo-secrets   Opaque   2      2m25s
$ kubectl get all
NAME                                    READY   STATUS    RESTARTS   AGE
pod/mongo-deployment-5fcf84768f-s8pz9   1/1     Running   0          2m24s
pod/web-deployment-fcc87bb9f-m6c8p      1/1     Running   0          2m13s

NAME                    TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)           AGE
service/kubernetes      ClusterIP   10.96.0.1       <none>        443/TCP           2m57s
service/mongo-service   NodePort    10.105.77.118   <none>        27017:30100/TCP   2m24s
service/web-service     NodePort    10.110.32.249   <none>        3000:30200/TCP    2m13s

NAME                               READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/mongo-deployment   1/1     1            1           2m24s
deployment.apps/web-deployment     1/1     1            1           2m13s

NAME                                          DESIRED   CURRENT   READY   AGE
replicaset.apps/mongo-deployment-5fcf84768f   1         1         1       2m24s
replicaset.apps/web-deployment-fcc87bb9f      1         1         1       2m13s
$ kubectl describe service web-service
Name:                     web-service
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app.kubernetes.io/name=web
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.110.32.249
IPs:                      10.110.32.249
Port:                     <unset>  3000/TCP
TargetPort:               3000/TCP
NodePort:                 <unset>  30200/TCP
Endpoints:                <none>
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
$ minikube ip
192.168.49.2
$ kubectl get node
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   41m   v1.30.0
$ kubectl get node -o wide
NAME       STATUS   ROLES           AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION    CONTAINER-RUNTIME
minikube   Ready    control-plane   41m   v1.30.0   192.168.49.2   <none>        Ubuntu 22.04.4 LTS   6.6.22-linuxkit   docker://26.0.1
$ 
```

### Troubleshoot

If you want to delete all configs and pods following these:

```
kubectl delete deployment --all
kubectl delete service --all
kubectl delete pod --all
kubectl delete configmap --all
kubectl delete secret --all
```