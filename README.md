# ArgoCD + Argo Workflow to Automate k8s resources deployment 

## Pre-req
- Install minikube

## Set-up
- Install argo cd
  - `kubectl create ns argocd`
  - `kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml` 
- Install argo workflow
  - `kubectl create ns argo`
  - `helm repo add argo https://argoproj.github.io/argo-helm`
  - `helm install argo-workflow argo/argo --version 0.16.7 --set installCRD=false -n argo`
- In setup folder I have added some nodeport service to expose the argocd-ui and workflow ui which you can access by IP of any node provided the right port
- Added an role to enable deployment of argoproj/application 
  - `cd setup`
  - `kubectl apply -f .`
- To list down endpoints
  - minikube service list
## Application
- Apply argocd appliaction which will run the worflow 
   - `kubectl apply -f argo-cd-workflow.yaml`
- This application run the dag worflow given in workflow folder with name dag.yaml
- This dag workflow will then run the application and install the helm chart 

