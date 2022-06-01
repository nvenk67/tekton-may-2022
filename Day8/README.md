# OpenShift CI/CD with Tekton

## What are the alternative Tekton CI/CD options available ?
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
