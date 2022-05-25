# Day 2 - OpenShift

## What are the chain of things that happens with Kubernetes/OpenShift when we deploy an application?
```
oc new-project jegan
oc create deploy nginx --image=bitnami/nginx:latest
```

1. oc/kubectl sends a request via a REST call to API Server to create a Deployment with the details given in the above command.
2. API Server receives the request from oc/kubectl and creates a new Deployment by name nginx in the etcd database.
3. API Server then triggers an event like "New Deployment created"
4. Deployment Controller then receives the event and sends a request to API Server to create a ReplicaSet for the new Deployment.
5. API Server receives the request from Deployment Controller and creates a ReplicaSet in the etcd database.
6. API Server then triggers an event like "New ReplicaSet created"
7. ReplicaSet Controller then receives the event and sends a request to API Server to create new Pods with the image=bitnami/nginx:latest container image.
8. API Server creates new Pod entries in the etcd database as requested by the ReplicaSet Controller
9. API Server triggers an event like "New Pod(s) created"
10. Scheduler receives the event, and identifies where the new Pods can be deployed and intimates API Server with the node scheduling recommendations
11. API Server then updates the Pod entries in etcd database with the scheduling details.
12. API Server triggers an event that Pods are scheduled to respective nodes as a broadcast event
13. kubelet container agents running on the respective nodes receives the broadcast event and if the node detail matches theirs, downloads the container images and creates the Pods with those container images, monitors the Pod health periodically and updates the API Server like a heart-beat update
14. API Server updates the Pod status as Running in the etcd based on the updates from the respective kubelet container agent notification.

## Listing the existing projects in OpenShift
```
oc get projects
```

## Finding the currently active project
```
oc project
```
The expected output is
<pre>
(root@tektutor.org)# oc project
Using project "jegan" on server "https://api.ocp.tektutor.org:6443".
</pre>


## Switching to a different project
```
oc project <any-other-existing-project-name>
```

## Scaling up your nginx deployment

List the number of nginx pods running
```
oc get po
```

Now you scale up the Pods to count 3
```
oc scale deploy/nginx --replicas=3
```

List the number of nginx pods running now

You are expected to see 3 replicas of nginx Pods after scale up

You may watch the pods status
```
oc get po -o wide -w
```
To come out of watch mode, you may hit Ctrl + c


## Kubernetes
- supports 3 types of services
  1. ClusterIP Service ( Internal service - ie works only with K8s cluster )
  2. NodePort Service ( External service -ie accessible even outside the K8s cluster )
  3. LoadBalancer Service ( External Service - used typically in cloud env like AWS/Azure, etc )
      - an external Load Balancer will be created which performan load balance to different Pods
      - on Prem if you need this, you need install MetalLB/Traeffic Load Balancer

## OpenShift
- built on top of Kubernetes with many additional features
- whatever works in Kubernetes also works in OpenShift
- supports a new feature called route that provides a friendly url for your services that can be accessed outside the cluster
