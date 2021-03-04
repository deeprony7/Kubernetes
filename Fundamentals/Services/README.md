# Services

* Pods are very **dynamic**, they come and go on the Kubernetes cluster
    * When using a **Replication Controller**, pods are terminated ad created during scaling operations
    * When using **Deployments**, when **updating** the image version, pods are **terminated** and new pods take the plcve of the older pods

* That's why Pods should never be accessed directly, but always through a **Service**
* A service is the **logical bridge** between the "mortal" pods and other **services** or **end-users**
* Creating a service will create an endpoint for your pods:
    * a **ClusterIP**: a virtual IP address only reachable from withing the cluster(default)
    * a **NodePort**: a port that is the same on each node that is also reachable externally
    * a **LoadBalancer**: a LoadBalancer created by the cloud provider that will route external traffic to every node in the NodePort (ELB on AWS)

* There is a possibility to add DNS names
    * **ExternalName** can provide a DNS name for the service

---

## Commands

`kubectl get node`
