## Installing tekton-polling-operator
Tekton Triggers depends on GitHub webhooks.  As OpenShift DNS routes and OpenShift webconsole in a baremetal setup 
aren't accessible from Internet to GitHub/GitLab, GitHub/GitLab webhooks will not be able to invoke Tektonpipeline. 

The tekton-polling-operator comes in handy for a bare-metal OpenShift setup.  This approach also works in cloud environments whether it is public/private/hybrid cloud.
```
oc apply -f https://github.com/bigkevmcd/tekton-polling-operator/releases/download/v0.4.0/release-v0.4.0.yaml
```

Expected output is
<pre>
(jegan@tektutor.org)$ <b>oc apply -f https://github.com/bigkevmcd/tekton-polling-operator/releases/download/v0.4.0/release-v0.4.0.yaml</b>
deployment.apps/tekton-polling-operator created
rolebinding.rbac.authorization.k8s.io/tekton-polling-operator created
role.rbac.authorization.k8s.io/tekton-polling-operator created
serviceaccount/tekton-polling-operator created
customresourcedefinition.apiextensions.k8s.io/repositories.polling.tekton.dev created
</pre>

## Create the java cicd tekton pipeline

You detailed instructions, you may refer my medium blog here 
<pre>
https://medium.com/tektutor/openshift-ci-cd-with-tekton-faa88ba45656
</pre>

The java cicd tekton pipeline depends on git-clone and maven tasks from Tekton Hub. Hence we need to install
those 2 Tasks as shown below
```
tkn hub install task git-clone
tkn hub install task maven
```

You may now create the tekton pipeline
```
cd ~/tekton-may-2022
git pull
cd Day10

oc apply -f java-tekton-cicd-pipeline.yml
```
Expected output is
<pre>
(jegan@tektutor.org)$ <b>oc apply -f java-tekton-cicd-pipeline.yml</b>
persistentvolume/tektutor-tekton-pv unchanged
persistentvolumeclaim/tektutor-tekton-pvc unchanged
pipeline.tekton.dev/java-cicd-pipeline unchanged
pipelinerun.tekton.dev/java-cicd-pipeline-run created
</pre>

You can try check the status of the java-cicd-pipeline-run from your OpenShift Pipeline webconsole.

## Triggering the pipeline based on code commit on the GitHub repo
```
cd ~/tekton-may-2022
git pull
cd Day10

oc apply -f git-trigger.yml
```

Expected output is
<pre>
(jegan@tektutor.org)$ <b>oc apply -f git-trigger.yml</b>
repository.polling.tekton.dev/tektutor-git-repo created
</pre>

You can watch the pipeline execution getting triggered from your Openshift Pipeline webconsole.

## For further learning

<pre>
https://cloud.google.com/kubernetes-engine/docs/concepts/persistent-volumes

https://docs.openshift.com/container-platform/4.10/installing/installing_bare_metal_ipi/ipi-install-troubleshooting.html

https://access.redhat.com/documentation/en-us/openshift_container_platform/4.8/html/cicd/pipelines
</pre>


tkn pipeline start  \
  --namespace=jegan \
  --serviceaccount=github-bot \
  --param private-github-repo-url='https://github.com/redhat-scholars/tekton-secretworld' \
  --workspace name=source,claimName=tekton-tutorial-sources \
  --use-param-defaults \
  --showlog
