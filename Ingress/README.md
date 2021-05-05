# Ingress Controller

* Run `kubectl apply -f ingress.yaml -f nginx-ingress-controller.yml -f helloworld-v1.yml -f echoservice.yml -f helloworld-v2.yml`
* Run `kubectl get pods` to check if all pods are running
* Once all of them start running, run `minikube ip` to get the endpoint
* Run `curl <ip-returned>`
* Run `curl 192.168.49.2 -H 'Host: helloworld-v1.example.com'` to simulate access over browser. `helloworld-v1.example.com` comes from ingress host
* Same goes with `curl 192.168.49.2 -H 'Host: helloworld-v2.example.com'`
* 