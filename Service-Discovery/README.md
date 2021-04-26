### Commands to excute:

```bash
kubectl delete all --all

kubectl get deployments
kubectl apply -f Service-Discovery/secrets.yaml
kubectl get secrets
kubectl apply -f Service-Discovery/database.yaml -f Service-Discovery/database-service.yaml
kubectl apply -f Service-Discovery/helloworld-db.yaml -f Service-Discovery/helloworld-db-service.yaml
kubectl get svc

minikube service helloworld-db-service --url
kubectl get pods

kubectl logs helloworld-deployment-6746b65c5f-5fhj9
curl http://192.168.49.2:31410
echo cm9vdHBhc3N3b3Jk | base64 -d
kubectl exec -it database -- mysql -u root -p

kubectl run -i --tty busybox --image=busybox:1.28 --restart=Never -- sh
-- nslookup [service-name]

kubectl delete pod busybox
```
