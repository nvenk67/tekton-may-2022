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

oc apply -f hello-service.yml
```
