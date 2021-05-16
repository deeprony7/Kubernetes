# Volumes
> Note: This wont work with your local Minikube setup

## Steps:
* Create a volume with ```aws --endpoint-url=http://localhost:4566 --profile=demo ec2 create-volume --size 10 --availability-zone us-east-1a --volume-type gp2 --tag-specifications 'ResourceType=volume, Tags=[{Key= KubernetesCluster, Value=kubernetes.domain.tld}]'```
* Run `kubectl apply -f Volumes/helloworld-w-volume.yaml` to map the volume
