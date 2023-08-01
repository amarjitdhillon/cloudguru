

A Kubernetes Service is a resource you create to make a single, constant point of entry to a group of pods providing the same service. Each service has an IP address and port that never change while the service exists. Clients can open connections to that IP and port, and those connections are then routed to one of the pods backing that service. This way, clients of service don’t need to know the location of individual pods providing the service, allowing those pods to be moved around the cluster at any time.




If we do an exec to service IP, then we will be able to exec to one of the pods backed by it

!!! info
    List the pods with the kubectl get pods command and choose one as your target for the exec command (in the following example, I've chosen the kubia-7nog1 pod as the target). You'll also need to obtain the cluster IP of your service (using kubectl get svc). When running the following commands yourself, be sure to replace the pod name and the service IP with your own:


```bash
kubectl exec kubia-7nog1 -- curl -s http://10.111.249.153
```


## NodePort 

By creating a NodePort service, you make Kubernetes `reserve a port` on all its nodes (the same port number is used across all of them) and forward incoming connections to the pods that are part of the service.

<center> <img src="../images/nodeport.png" width="70%"> </center>

!!! remember
    - NodePort service can be accessed through the service's internal cluster IP and through any node's IP and the reserved node port
    - Specifying the port isn’t mandatory; Kubernetes will choose a random port if you omit it.


### Example

```bash
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app.kubernetes.io/name: MyApp
  ports:
      # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
    - port: 80
      targetPort: 80
      # Optional field
      # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
      nodePort: 30007
```


## ClusterIP

To make the pod accessible from the outside, we need to expose it through a `Service` object. You’ll create a special service of type `LoadBalancer`, because if you create a regular service (a `ClusterIP service`), like the pod, it would also only be accessible from inside the cluster. By creating a LoadBalancer-type service, an external load balancer will be created and you can connect to the pod through the load balancer’s public IP.

==The ClusterIP provides a load-balanced IP address. One or more pods that match a label selector can forward traffic to the IP address. The ClusterIP service must define one or more ports to listen on with target ports to forward TCP/UDP traffic to containers. The IP address that is used for the ClusterIP is not routable outside of the cluster, like the pod IP address is==



## LoadBalancer

Kubernetes clusters running on cloud providers usually support the automatic provision of a load balancer from the cloud infrastructure. All you need to do is set the service’s type to LoadBalancer instead of NodePort. The load balancer will have its own unique, publicly accessible IP address and will redirect all connections to your service. You can thus access your service through the load balancer’s IP address


```bash
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  clusterIP: 10.0.171.239
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - ip: 192.0.2.127
```

!!! warning
    Some cloud providers allow you to specify the loadBalancerIP. In those cases, the load-balancer is created with the user-specified loadBalancerIP. If the loadBalancerIP field is not specified, the loadBalancer is set up with an ephemeral IP address. If you specify a loadBalancerIP but your cloud provider does not support the feature, the loadbalancerIP field that you set is ignored.

