# Day 4


## Creating a deployment manifest file from command line
```
oc create deploy hello --image=tektutor/hello:1.0 --dry-run -o yaml > hello-deploy.yml
```

## Creating deployment from yaml file from GitHub
```
oc apply -f https://github.com/tektutor/sample-openshift-app/blob/main/hello-deploy.yml
```

## Get help about any kind of Resource within OpenShift
```
oc explain deployment
```

## Creating application deployments in declarative style

Delete any existing deployment in the name hello if exists
```
oc delete deploy/hello
```

Let's create the hello deployment as shown below
```
cd ~
git clone https://github.com/tektutor/tekton-may-2022.git
cd tekton-may-2022/Day4/manifests

oc apply -f hello-deploy.yml
```

List and see if the hello deploy is created as expected
```
oc get deploy
```

## Creating a clusterip service for the hello deployment in declarative style
Clean up any service in the name hello(if any)
```
oc delete svc/hello
```

Now let's create the cluster-ip internal service for hello via manifest file
```
cd ~/tekton-may-2022
git pull
cd Day4/manifests

oc apply -f hello-clusterip-service.yml
```

You can open a shell or get inside a Pod 
```
oc exec -it hello-7484667c7d-4wl9w sh
```

From within the Pod shell, you can access the clusterip service as shown below
```
curl 172.30.223.164:8080
curl hello:8080
```

## Creating a nodeport service for the hello deployment in declarative style
Clean up any service in the name hello(if any)
```
oc delete svc/hello
```
Alternatively, you can delete the clusterip service in declarative style
```
oc delete -f hello-clusterip-service.yml
```

Now let's create the nodeport external service for hello via manifest file
```
cd ~/tekton-may-2022
git pull
cd Day4/manifests

oc apply -f hello-nodeport-service.yml
```

## Creating a loadbalancer service for the hello deployment in declarative style
Clean up any service in the name hello(if any)
```
oc delete svc/hello
```

Alternatively, you can delete the nodeport service in declarative style
```
oc delete -f hello-nodeport-service.yml
```


Now let's create the loadbalancer external service for hello via manifest file
```
cd ~/tekton-may-2022
git pull
cd Day4/manifests

oc apply -f hello-loadbalancer-service.yml
```
