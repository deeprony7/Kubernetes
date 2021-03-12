# Pod Lifecycle

This deployment is to check how and what lifecycle stages does a pod have and how we can perform a lifecycle hook

* Run the deployment and watch the pod state
```
kubectl apply -f Fundamentals/Pod-lifecycle/lifecycle.yaml && watch -n1 kubectl get pods
```

* Once the pod shows up, perform and exec to look at the timing file which has the time logs in epoch
```
kubectl exec -it lifecycle-565888dd66-dxkpf -- tail /timing -f 
```
Output:
```bash
1615573893: Running
1615573894: postStart
1615573904: end postStart
1615573932: livenessProbe
1615573936: readinessProbe
1615573942: livenessProbe
1615573946: readinessProbe
1615573952: livenessProbe
1615573956: readinessProbe
1615573962: livenessProbe
1615573966: readinessProbe
1615573972: livenessProbe
1615573976: readinessProbe
1615573982: livenessProbe
1615573986: readinessProbe
1615573992: livenessProbe
1615573996: readinessProbe
1615574002: livenessProbe
1615574006: readinessProbe
1615574012: livenessProbe
command terminated with exit code 137
```