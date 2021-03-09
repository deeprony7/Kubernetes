# NodeSelector using Labels

* get nodes `kubectl get nodes --show-labels`

* create the deployment `kubectl create -f hw-nodeselector.yaml`

* check deployments `kubectl get deployments`

* check and describe one of the pod it spawns
```
kubectl get pods
kubectl describe pods hw-deployment-8fd77c9c8-r7lqd
```
And you will see that it failed to start as it didnt find a matching label

* now lets add the matching label with
`kubectl label nodes minikube hardware=high-spec`

* verify that with `kubectl get nodes --show-labels`
And you shall see the label in LABELS

* You will now find that the pods are now starting - check one of them with `kubectl describe pods hw-deployment-8fd77c9c8-r7lqd`
