# Day 4


## Creating a deployment manifest file from command line
```
oc create deploy hello --image=tektutor/hello:1.0 --dry-run -o yaml > hello-deploy.yml
```

## Creating deployment from yaml file from GitHub
```
oc apply -f https://github.com/tektutor/sample-openshift-app/blob/main/hello-deploy.yml
```
