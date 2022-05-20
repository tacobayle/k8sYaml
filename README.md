# useful K8S commands

## create a Pod

```
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sPodRadialBusyBoxPlusCurl.yml
pod/busybox created
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl get pod -o wide
NAME                                READY   STATUS    RESTARTS   AGE   IP           NODE      NOMINATED NODE   READINESS GATES
busybox                             1/1     Running   0          13s   10.244.2.5   bionic2   <none>           <none>
nginx-deployment-7c9f54d5f9-bclhm   1/1     Running   0          16h   10.244.1.3   bionic3   <none>           <none>
nginx-deployment-7c9f54d5f9-grttz   1/1     Running   0          16h   10.244.2.3   bionic2   <none>           <none>
nic@bionic1:~$
```

## create a deployment (nginx)

```
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sDeploymentNginx.yml
deployment.apps/nginx-deployment created
nic@bionic1:~$
nic@bionic1:~$ kubectl get deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   2/2     2            2           8s
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl get deployment
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   2/2     2            2           14s
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl get pods -o wide
NAME                                READY   STATUS    RESTARTS   AGE   IP           NODE      NOMINATED NODE   READINESS GATES
nginx-deployment-7c9f54d5f9-bclhm   1/1     Running   0          21s   10.244.1.3   bionic3   <none>           <none>
nginx-deployment-7c9f54d5f9-grttz   1/1     Running   0          21s   10.244.2.3   bionic2   <none>           <none>
nic@bionic1:~$
nic@bionic1:~$
```

## create a deployment (busybox - basic webserver) with service

```
nic@bionic1:~$
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sDeploymentBusyBoxFrontEndV1.yml
deployment.apps/web-front created
nic@bionic1:~$
nic@bionic1:~$ kubectl get deployment -o wide
NAME        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES               SELECTOR
web-front   3/3     3            3           76s   web-front    k8s.gcr.io/busybox   app=web-front
nic@bionic1:~$
nic@bionic1:~$ kubectl get pods -o wide
NAME                         READY   STATUS    RESTARTS   AGE   IP            NODE      NOMINATED NODE   READINESS GATES
web-front-58fdbdf559-5t75h   1/1     Running   0          42s   10.244.1.22   bionic3   <none>           <none>
web-front-58fdbdf559-qrqtl   1/1     Running   0          42s   10.244.2.18   bionic2   <none>           <none>
web-front-58fdbdf559-wfvwh   1/1     Running   0          42s   10.244.1.23   bionic3   <none>           <none>
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sServiceBusyBoxFrontEndV1.yml
service/web-front created
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl get svc
NAME         TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1       <none>        443/TCP        19h
web-front    NodePort    10.107.27.252   <none>        80:30731/TCP   7s
nic@bionic1:~$
```

## scale a deployment

```
nic@bionic1:~$
nic@bionic1:~$ kubectl get deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
nginx-deployment   2/2     2            2           20h   nginx        nginx:1.15.4   app=nginx
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl scale deployment/nginx-deployment --replicas=4
deployment.apps/nginx-deployment scaled
nic@bionic1:~$
nic@bionic1:~$ kubectl get deployment -o wide
NAME               READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES         SELECTOR
nginx-deployment   4/4     4            4           20h   nginx        nginx:1.15.4   app=nginx
nic@bionic1:~$
nic@bionic1:~$
```

## label a pod

kubectl label pods --overwrite nginx-deployment-7c9f54d5f9-grttz app=nginx

## 3 types of service:

### create a nodetype service

```
nic@bionic1:~$
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sServiceNodePortNginx.yml
service/nginx-service created
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$
nic@bionic1:~$ kubectl get services -o wide
NAME            TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE     SELECTOR
kubernetes      ClusterIP   10.96.0.1     <none>        443/TCP        5h29m   <none>
nginx-service   NodePort    10.97.30.52   <none>        80:30080/TCP   25s     app=nginx
nic@bionic1:~$
```


### create a LoadBalancer service

```
nic@bionic1:~$
nic@bionic1:~$ kubectl apply -f https://raw.githubusercontent.com/tacobayle/k8sYaml/master/k8sServiceLoadBalancerNginx.yml
service/nginx-loadbalancer created
nic@bionic1:~$
nic@bionic1:~$ kubectl get services -o wide
NAME                 TYPE           CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE     SELECTOR
kubernetes           ClusterIP      10.96.0.1       <none>        443/TCP        5h30m   <none>
nginx-loadbalancer   LoadBalancer   10.104.94.225   <pending>     80:30769/TCP   4s      app=nginx
nginx-service        NodePort       10.97.30.52     <none>        80:30080/TCP   83s     app=nginx
nic@bionic1:~$
```
