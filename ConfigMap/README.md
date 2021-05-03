# ConfigMap

- Create configmap ```kubectl create configmap nginx-config --from-file=reverseproxy.conf```
- ```kubectl get configmap```
- Read the contents of the configmap with: ```kubectl get configmap nginx-config -o yaml```
- Create Nginx pod with 2 containers - nginx and the node app ```kubectl apply -f nginx.yaml -f nginx-service.yaml```
- Get endpoint ```minikube service helloworld-nginx-service --url```
- Lets access the nginx container ```kubectl exec -it helloworld-nginx -c nginx -- bash```
- Run `ps -ef` check nginx process running
- You will also find the reverseproxy at `cat /etc/nginx/conf.d/reverseproxy.conf`