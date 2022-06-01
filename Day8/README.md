# OpenShift CI/CD with Tekton

## Tekton Overview
- Tekton is a Kubernetes native CI/CD Framework that also works pretty smoothly in OpenShift
- Tekton pipeline works in onPrem, public and private cloud as it is a native applications
  that run within OpenShift
- Tekton CI/CD framework is a open source project backed by RedHat
- OpenShift being a RedHat's product, RedHat also provides support for Tekton native CI/CD Pipeline to its customers
- Tekton adds many Custom Resources to OpenShift via Custom Resource Definitions (CRDs)
- To name a few Tekton Custom Resources
    - Tasks
    - TaskRuns
    - ClusterTasks
    - ClusterInterceptors
    - Conditions
    - PipelineResources
    - Repositories
    - Runs
    - TektonAddons
    - TektonConfigs
    - TektonHubs
    - Pipelines
    - PipelineRuns
    - Workspaces
    - TektonTriggers
    - TektonBindings
    - TektonTemplates

- Tekton also adds Custom Controllers to manage the above Custom Resources
- Tekton can be installed easily in OpenShift from the Operator Hub by installed "Red Hat OpenShift Tekton Operator"
- Tekton allows to create pipelines via webconsole GUI or via declarative yaml script

## What are the Tekton CI/CD alternative options available ?
- Jenkins
- Jenkins-x
- GitHub Actions
- CircleCI
- GitLab CI
- Codeship
- Travis CI
- TeamCity
- Azure Pipelines

## Advantage of Tekton over Jenkins
- Jenkins declarative pipeline uses Groovy
- Tekton pipelines can be created using YAML, hence learning additional programming language is not necessary
- Jenkins uses Plugins for everything, in case of plugin conflicts customer can't expect any support
- Tekton is backed by RedHat, hence RedHat wordwide support is guaranteed
- Tekton is servless
- Jenkins CI/CD should be running 24x7 to detect code changes and to run pipeline

## Advantage of Tekton over Travis CI
- Travis CI can't be hosted on-prem
- Tekton works in cloud or on-prem
- Travis CI is unstable and not backed by support
- Tekton CI/CD is stable and backed by RedHat wordwide support
- Travis CI container image and dependencies are messy 
- Tekton images are comparatively thin and comes from RedHat Container Registry

## Advantage of Tekton over Circle CI
- Circle CI is unstable and expensive while Tekton is stable and a opensource Framework backed with RedHat support
- Circle CI is more suitable for cloud while Tekton works in cloud and on-prem setups

## Advantage of Tekton over GitLab CI
- GitLab CI works well for customers already using GitLab Code Repository
- New customer will have to migrate their source code to GitLab in order to use GitLab CI, which the customers
  tied to one vendor
- Using Tekton CI/CD doesn't require any code migration
- As most of the organizations are already using OpenShift, using Tekton CI/CD is a natural choice
  as it doesn't come with any additional effort or cost to use Tekton

## Advantage of Tekton over TeamCity
- TeamCity is not a open source while Tekton is open source but Tekton is backed by RedHat support
- TeamCity becomes more expensive for CI/CD that involves more than 3 agents
- Tekton doesn't have any such restrictions

## Advantage of Tekton over CodeShip
- Codeship GUI isn't user-friendly
- Codeship isn't free for commercial use
- Tekton is free for opensource and commercial projects
- Tekton can be used in open source Kubernetes as well as RedHat OpenShift
- Codeship doesn't support ios builds but Tekton support ios application builds natively.

## Advantage of Tekton over GitHub Actions
- GitHub Actions doesn't seem to support manual pipeline trigger
- Tekton supports triggering pipeline both manually and via external triggers like code commit, etc.,
- GitHub Actions is tightly integrated to GitHub code Repository
- Tekton Pipelines can utilize source code from any type of Code Repository including GitHub
- GitHub Actions supports only cloud setup while Tekton works in on-prem too

## Some additional points to think 
- Tekton is a Kubernetes native Framework that is built on top of Kubernetes/OpenShift API
  by adding Custom Resources like Task, TaskRun, Pipeline, PipelinRun, Workspaces, etc.,

- Tekton is serverless and works pretty well in on-prem, public and private clouds, supporting every
  type of environment

- GitHub Actions CI/CD is tightly coupled with GitHub, while Tekton isn't restricted to GitHub as Tekton 
  works well with any type of Version control including GitHub, GitLab, etc.,

- GitHub Actions requires your code kept in one of the GitHub repository, while Tekton allows one to perform CI/CD
  even in on-prem infra without leaving your organization network as OpenShift allows hosting your
  own private GitHub like Code Repository within OpenShift

- Gitlab also plans to integrate with Tekton 

- Jenkins-x uses Tekton CI/CD


## Tekton CI/CD Pipeline

- each pipeline is a combination of many tasks executed sequentially or parallely
- Task is an independently executable unit in Tekton
- Each Task will create a Pod
- Tasks are further broken down into Steps
- Steps can only executed as part a Task, hence we can't execute steps independently outside Tasks
- Each Step creates a Container within the Task Pod
- Steps uses Workspaces as directories to read and write files
- Steps takes certain inputs from the workspace and then can pass on their output to other Steps by writing
  their output to the Workspace directory
- Worskpaces can be shared by one or more steps or by different Tasks
- Each Task can be executed by creating a TaskRun
- TaskRun provides necessary configuration and parameters values to the Task for execution
- Each Pipeline can be executed by creating a PipelineRun
- PipelineRun provides necessary configuration and parameter values(if any) to the Pipeline
- TaskRun represents one execution of a Task
- each time you execute a Task, a separate TaskRun will be created
- each time you execute a Pipeline, a separate PipelineRun will be created
- Taskrun or the PipelineRun stores the logs generated while executed the TaskRun/PipelineRun

## RedHat Container Registry URL
<pre>
https://catalog.redhat.com/software/containers/search
</pre>

## Creating your first Tekton Task
```
cd ~/tekton-may-2022
git pull

cd Day8/tekton
oc apply -f task-1.yml 
```

Expected output is
<pre>
[jegan@localhost tekton]$ <b>oc apply -f task-1.yml</b>
task.tekton.dev/hello-world-task created
</pre>

## Listing the Tekton tasks
```
oc get tasks
oc get task

tkn tasks list
tkn task list
tkn t list
```

## Creating a TaskRun to execute the task we created just now
```
cd ~/tekton-may-2022
git pull

cd Day8/tekton
oc apply -f helloworld-taskrun.yml 
```

Expected output
<pre>
[jegan@localhost tekton]$ <b>oc apply -f helloworld-taskrun.yml</b>
taskrun.tekton.dev/helloworld-taskrun created
</pre>

## Checking the output logs of taskrun
```
tkn tr list
tkn logs helloworld-taskrun
```
Expected output is
<pre>
[jegan@localhost tekton]$ <b>tkn tr list</b>
NAME                 STARTED          DURATION     STATUS
helloworld-taskrun   15 seconds ago   11 seconds   Succeeded
[jegan@localhost tekton]$ <b>tkn tr logs helloworld-taskrun</b>
[hello-world] Hello TekTon !
</pre>
