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
The expected output is
<pre>
(jegan@tektutor.org)$ oc explain deployment
KIND:     Deployment
VERSION:  apps/v1

DESCRIPTION:
     Deployment enables declarative updates for Pods and ReplicaSets.

FIELDS:
   apiVersion	<string>
     APIVersion defines the versioned schema of this representation of an
     object. Servers should convert recognized schemas to the latest internal
     value, and may reject unrecognized values. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#resources

   kind	<string>
     Kind is a string value representing the REST resource this object
     represents. Servers may infer this from the endpoint the client submits
     requests to. Cannot be updated. In CamelCase. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#types-kinds

   metadata	<Object>
     Standard object's metadata. More info:
     https://git.k8s.io/community/contributors/devel/sig-architecture/api-conventions.md#metadata

   spec	<Object>
     Specification of the desired behavior of the Deployment.

   status	<Object>
     Most recently observed status of the Deployment.
<pre>
