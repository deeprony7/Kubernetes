# ConfigMap

- Create configmap ```kubectl create configmap nginx-config --from-file=reverseproxy.conf```
- ```kubectl get configmap```
- Read the contents of the configmap with: ```kubectl get configmap nginx-config -o yaml```
- 