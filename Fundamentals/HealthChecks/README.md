# Heathchecks

Healthchecks are important to check the health of the pods and have kubernetes stop routing traffic to unhealthy pod and spin up a new one.

### Liveness

* Create deployment with `kubectl create -f Fundamentals/HealthChecks/hw-healthcheck.yaml`

* Lets describe one of the pod
```bash
kubectl get pods
watch kubectl get pods 
kubectl describe pods hw-deployment-7f49fbb9cc-czsrr
```

* When a __describe__ is done below output shows with the liveness details

```bash
    Requests:
      cpu:        500m
      memory:     128Mi
    Liveness:     http-get http://:nodejs-port/ delay=15s timeout=30s period=10s #success=1 #failure=3
    Environment:  <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from default-token-r7256 (ro)
```
---

### Readiness

Readiness differs from Liveness in the sense, that it waits to see id the pod is actually ready to respond to requests only then does it route traffic to that pod. It does not however kill the pod.

> Failing liveness probe will restart the container, whereas failing readiness probe will stop our application from serving traffic.

```
kubectl create -f Fundamentals/HealthChecks/hw-liveness-readiness.yaml && watch -n 1 kubectl get pods
```
Of course, remove watch command if not interested in viewing the pods immediately.
