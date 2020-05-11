# usefulTips.md

## create a deployment

```nic@bionic1:~$
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

## label a pod

kubectl label pods --overwrite nginx-deployment-7c9f54d5f9-grttz app=nginx

## 3 types of service:

### create a nodetype service

```

```


### create a LoadBalancer service
```
```
