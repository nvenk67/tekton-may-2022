## Task with multiple steps
- Tekton creates a separate Pod for each Task
- Tekton creates a container for each step in a Task
- Let's say a Tekton Task has 3 steps, then Tekton will create 3 containers within the Task pod
- The step containers are executed in sequence from top to bottom
- When a previous step fails, the subsequent steps will be skipped
- Related steps can be put together in a single Task
- One Task should do only major functionality
- For example, cloning source code can be done as a single task
- Compiling the source code should be done as a separate Task

## Pipeline with Multiple Tasks
- Tekton creates separate Pods for each Task in a Pipeline
- Tasks in a Pipeline can be executed either in sequence or in parallel as per our instructions in the pipeline

## Encoding the values to be stored in secrets 
It is important to use -n switch in echo command, otherwise echo will add a newline character by default.
Hence the newline character also will get encoded. The -n switch ensure no newline character is appended by echo.
```
echo -n root|base64
echo -n Admin@123|base64
```

Expected output
<pre>
(jegan@tektutor.org)$ echo -n root|base64
cm9vdA==
(jegan@tektutor.org)$ echo -n Admin@123|base64
QWRtaW5AMTIz
</pre>

You may now add the above encoded strings in a secret
```
apiVersion: v1
kind: Secrets
metadata:
  name: mysql-login-credentials
data:
  user: cm9vdA==
  password: QWRtaW5AMTIz
```

## Lab Exercise - Creating a task that fetches login credentials from secrets mounted as a Volume
```
cd ~/tekton-may-2022
git pull

cd Day9
oc apply -f task-that-mounts-secrets-as-volume.yml
``` 

Expected output
<pre>
(jegan@tektutor.org)$ <b>oc apply -f task-that-mounts-secrets-as-volume.yml</b>
secret/mysql-login-credentials unchanged
task.tekton.dev/task-with-secrets created
</pre>

#### List the task
```
tkn task list
```
Expected output is
<pre>
(jegan@tektutor.org)$ <b>tkn task list</b>
NAME                DESCRIPTION   AGE
task-with-secrets                 57 seconds ago
</pre>

#### Running the task
```
tkn task start task-with-secrets
```
Expected output
<pre>
(jegan@tektutor.org)$ tkn task start task-with-secrets
TaskRun started: task-with-secrets-run-2dbdn

In order to track the TaskRun progress run:
tkn taskrun logs task-with-secrets-run-2dbdn -f -n default
</pre>

#### Checking the taskrun output logs
The command below will show the logs of the last executed taskrun
```
tkn taskrun logs -f --last
```
Expected output
<pre>
(jegan@tektutor.org)$ tkn taskrun logs -f --last
[unnamed-0] total 0
[unnamed-0] lrwxrwxrwx. 1 root root  11 Jun  2 03:37 user -> ..data/user
[unnamed-0] lrwxrwxrwx. 1 root root  15 Jun  2 03:37 password -> ..data/password
[unnamed-0] lrwxrwxrwx. 1 root root  32 Jun  2 03:37 ..data -> ..2022_06_02_03_37_29.2607677157
[unnamed-0] drwxr-xr-x. 2 root root  80 Jun  2 03:37 ..2022_06_02_03_37_29.2607677157
[unnamed-0] drwxrwxrwt. 3 root root 120 Jun  2 03:37 .
[unnamed-0] drwxr-xr-x. 1 root root  21 Jun  2 03:37 ..
[unnamed-0] 
[unnamed-0] root
[unnamed-0] Admin@123
</pre>

## Lab Exercise - Task that retrieves values from ConfigMap mounted as a Volume
```
cd ~/tekton-may-2022
git pull

cd Day9
oc apply -f task-that-mounts-configmap-as-volume.yml 
``` 

Expected output
<pre>
(jegan@tektutor.org)$ oc apply -f task-that-mounts-configmap-as-volume.yml 
configmap/my-config-map created 
task.tekton.dev/task-with-configmap created
</pre>

#### Listing the tasks
```
tkn task list
```
Expected output
<pre>
(jegan@tektutor.org)$ tkn task list
NAME                  DESCRIPTION   AGE
<b>task-with-configmap                 1 minute ago</b>
task-with-secrets                   8 minutes ago
</pre>

### Executing the Task
```
tkn task start task-with-secrets --showlog
```

Expected output
<pre>
(jegan@tektutor.org)$ tkn task start task-with-configmap --showlog
TaskRun started: task-with-configmap-run-6pjgl
Waiting for logs to be available...
[unnamed-0] total 0
[unnamed-0] lrwxrwxrwx. 1 root root 14 Jun  2 03:51 m2_home -> ..data/m2_home
[unnamed-0] lrwxrwxrwx. 1 root root 15 Jun  2 03:51 jdk_home -> ..data/jdk_home
[unnamed-0] lrwxrwxrwx. 1 root root 32 Jun  2 03:51 ..data -> ..2022_06_02_03_51_49.4159107458
[unnamed-0] drwxr-xr-x. 2 root root 37 Jun  2 03:51 ..2022_06_02_03_51_49.4159107458
[unnamed-0] drwxrwxrwx. 3 root root 91 Jun  2 03:51 .
[unnamed-0] drwxr-xr-x. 1 root root 23 Jun  2 03:51 ..
[unnamed-0] 
[unnamed-0] /usr/share/maven
[unnamed-0] /usr/lib/jdk8
</pre>
