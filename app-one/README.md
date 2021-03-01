### Commands Run

* `kubectl create -f app-one/helloPod.yaml` to create pod

* `kubectl get pods` to get a list of pods

* `kubectl describe pod hellopod` and check the bottom section for events

* `kubectl port-forward hellopod 8081:3000` to forward container port so we can check locally with `curl localhost:8081`

**If you are on minikube:**

* `kubectl expose pod hellopod --type=NodePort --name hellopod-service`

* `minikube service hellopod-service` or `minikube service hellopod-service --url` to just get the url

