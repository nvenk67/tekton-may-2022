tkn pipeline start secretworld-app-clone \
  --namespace=workspace-auth-demo \
  --serviceaccount=github-bot \
  --param private-github-repo-url='https://github.com/redhat-scholars/tekton-secretworld' \
  --workspace name=source,claimName=tekton-tutorial-sources \
  --use-param-defaults \
  --showlog
