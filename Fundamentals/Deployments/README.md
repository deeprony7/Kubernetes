# Deployments

* Create Deployment `kubectl create -f Fundamentals/Deployments/hw-deployment.yaml`

* Check deployments
```
kubectl get deployments
NAME            READY   UP-TO-DATE   AVAILABLE   AGE
hw-deployment   3/3     3            3           28s
```

* Check Replication Sets
```
kubectl get rs
NAME                       DESIRED   CURRENT   READY   AGE
hw-deployment-558c5bd597   3         3         3       56s
```

* Check the pods created
```
kubectl get pods --show-labels
NAME                             READY   STATUS    RESTARTS   AGE     LABELS
hw-deployment-558c5bd597-9mqrg   1/1     Running   0          2m59s   app=hw-deployment,pod-template-hash=558c5bd597
hw-deployment-558c5bd597-ftg6w   1/1     Running   0          3m      app=hw-deployment,pod-template-hash=558c5bd597
hw-deployment-558c5bd597-kllcz   1/1     Running   0          2m59s   app=hw-deployment,pod-template-hash=558c5bd597
```


* Check rollout status
```
kubectl rollout status deployment/hw-deployment
deployment "hw-deployment" successfully rolled out
```

* Expose deplloyment
```
kubectl expose deployment hw-deployment --type=NodePort
service/hw-deployment exposed
```

* Get Services 
```
kubectl get svcNAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
hw-deployment   NodePort    10.104.229.128   <none>        3000:30397/TCP   62s
kubernetes      ClusterIP   10.96.0.1        <none>        443/TCP          24h
```

* Describe Service
```
kubectl describe svc hw-deployment
Name:                     hw-deployment
Namespace:                default
Labels:                   <none>
Annotations:              <none>
Selector:                 app=hw-deployment
Type:                     NodePort
IP Families:              <none>
IP:                       10.104.229.128
IPs:                      10.104.229.128
Port:                     <unset>  3000/TCP
TargetPort:               3000/TCP
NodePort:                 <unset>  30397/TCP
Endpoints:                172.17.0.3:3000,172.17.0.4:3000,172.17.0.5:3000
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

* Check url for the service
```
minikube service hw-deployment --url
http://192.168.49.2:30397
```

* Lets update the image tag
```
kubectl set image Deployments/hw-deployment k8s-demo=wardviaene/k8s-demo:2            
deployment.apps/hw-deployment image updated
```

* Check rollout status
```
kubectl rollout status deployment/hw-deployment
```

* curl nodeport
```
curl http://192.168.49.2:30397
Hello World v2!
```

* This has updated all our pods too
```
kubectl get podsNAME                             READY   STATUS    RESTARTS   AGE
hw-deployment-56b9478b4f-7n42m   1/1     Running   0          116s
hw-deployment-56b9478b4f-89kfc   1/1     Running   0          2m22s
hw-deployment-56b9478b4f-tvljq   1/1     Running   0          2m5s
```

* Check rollout history
```
 kubectl rollout history deployment/hw-deployment
deployment.apps/hw-deployment 
REVISION  CHANGE-CAUSE
1         <none>
2         <none>
```

Change cause does not show up as we did not use the `--record`  flag when creating the deployment

* Lets say we are not happy with this current version so lets rollback the changes
```
kubectl rollout undo deployment/hw-deployment
deployment.apps/hw-deployment rolled back

curl http://192.168.49.2:30397               
Hello World v2!                                                                       
kubectl rollout status deployment/hw-deployment

Waiting for deployment "hw-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "hw-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "hw-deployment" rollout to finish: 2 out of 3 new replicas have been updated...
Waiting for deployment "hw-deployment" rollout to finish: 1 old replicas are pending termination...
Waiting for deployment "hw-deployment" rollout to finish: 1 old replicas are pending termination...
deployment "hw-deployment" successfully rolled out

curl http://192.168.49.2:30397                 
Hello World!
```
Successfully rolled back easily.
This again will recreate the pods.

```
kubectl rollout history deployment/hw-deployment
deployment.apps/hw-deployment 
REVISION  CHANGE-CAUSE
2         <none>
3         <none>
```

* After making a bunch of these revisions, if we want to switch to a particular revision
```
kubectl rollout history deployment/hw-deployment                          
deployment.apps/hw-deployment 
REVISION  CHANGE-CAUSE
3         <none>
4         <none>
5         <none>


kubectl rollout undo deployment/hw-deployment --to-revision=3   deployment.apps/hw-deployment rolled back
```