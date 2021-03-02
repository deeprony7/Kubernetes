# Replication Controller

* Check kubectl node
`kubectl get node`

* Create the replication controller from the yaml
`kubectl create -f ReplicationController.yaml`

* `kubectl get pods`

* Describe a pod 
`kubectl describe pod hello-controller-68hg8`

* Try deleting and you will see K8s scale it back to 2 replicas
`kubectl delete pod hello-controller-68hg8`

* Set scale to 4 replicas
`kubectl scale --replicas=4 -f ReplicationController.yaml`

* Another way to scale:
get the name of the Replication Controller with `kubectl get rc`
`kubectl scale --replicas=1 -rc/hello-controller`

Output:
```bash
kubectl get podsNAME                     READY   STATUS        RESTARTS   AGE
hello-controller-49s2v   1/1     Terminating   0          2m58s
hello-controller-9kfdw   1/1     Terminating   0          2m58s
hello-controller-h87h2   1/1     Terminating   0          4m45s
hello-controller-vwxkb   1/1     Running       0          11m
```

* This horizontal scaling is only possible when you have **stateless** pods not possilbe with **stateful** pods

* To delete the replication controller `kubectl delete rc/hello-controller`