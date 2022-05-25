Day 3


# What is a Kubernetes/OpenShift Service?

- Service represents a group of similar Pods( Pods from same Deployment )
- all the pods in a Service will have same labels
- label selector is used to identify the Pods that belong to a particular service
- Service offers load-balancing to the group of Pods (Pods from same Deployment )
- You can create a Service for a group of nginx Pods
- You can create another Service for a group of tomcat Pods
- Yet another for mysql Pods

# What is an Ingress?
- ingress is a routing rule
- Ingress is a Kubernetes feature which also works in OpenShift
- For example
  www.tekutor.org - This should take me to Home Page
  www.tektutor.org/login - This url should invoke Login service
  www.tektutor.org/logout - This url should invoke Logout service
  www.tektutor.org/blog - This url should invoke the blog service

If you notice above, based on the url path, the call is routed to different services within the website

For Ingress to work in Kubernetes/OpenShift, we need an Ingress Controller.

Ingress Controller if present in the OpenShift/Kubernetes Cluster, it listens for new Ingress rules created
in the Cluter.
Whenever it detects new Ingress/updated Ingress rules, the Ingress Controller picks the ingress rules
and configures the Load Balancer to perform the routing to the corresponding service.

1. Load Balancer ( Nginx, HAProxy, etc., )
2. Ingress Controller 
   - In Managed OpenShift Service from AWS/AZure,Ingress Controller comes out of the box
5. Ingress Rule ( This is defined by Web Developer/DevOps Engineer )

# What is a route?
- OpenShift feature which isn't present Kubernetes
- In OpenShift, every service is generally created as clusterip service
- If service will be accessed externally, then a route will be created for the clusterIP service.
- If the service is accessed only within the cluster, then no route is created
- route only forwards the call to a single service
