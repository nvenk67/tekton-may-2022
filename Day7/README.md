## Understanding deployments using configmaps

Create the config map that has password
```
cd ~/tekton-may-2022
git pull
cd Day7/configmap-and-secrets

oc apply -f mysql-configmap.yml 
```

Create the persistent volume and claim
```
cd ~/tekton-may-2022
git pull
cd Day7/configmap-and-secrets

oc apply -f mysql-pv.yml 
oc apply -f mysql-pvc.yml 
```

Create the mysql deploy that retreives password from configmap
```
oc delete -f mysql-deploy.yml
oc apply -f mysql-deploy-with-configmap.yml
```

## Understanding deployments using secrets 

Ideally configmap must be used to store non-sensitive data like log file path, JDK_HOME path, etc. Secrets is the perfect
recommended way to store sensitive data in an encrypted fashion inside OpenShift.

Create the secret that has password
```
cd ~/tekton-may-2022
git pull
cd Day7/configmap-and-secrets

oc apply -f mysql-secrets.yml 
```

Create the mysql deploy that retreives password from secrets 
```
oc delete -f mysql-deploy-with-configmap.yml
oc apply -f mysql-deploy-with-secrets.yml
```

## Ingress

To enable Ingress Controller in RedHat OpenShift, we need to install Nginx Ingress Operator.  If you wish to enable Nginx Ingress Controller for a Kubernetes cluster you may read my medium blog at the URL below
<pre>
https://medium.com/tektutor/using-nginx-ingress-controller-in-kubernetes-bare-metal-setup-890eb4e7772
</pre>


# Pipeline

RedHat OpenShift supports CI/CD.  We need to install the knative opensource Tekton pipeline operator to create CI/CD pipelines.

For detailed instructions, you may read my medium blog here
<pre>
https://medium.com/tektutor/openshift-ci-cd-with-tekton-faa88ba45656
</pre>



