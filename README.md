### flask app v3 for testing kubernetes deployments.

#### CI/CD pipelines

CI/CD pipelines have been configured in github actions to create an image targeting the specific application folder. The pipeline 

- builds an image and 
- pushes the image to the docker hub - it can be azure container  or aws container registry

#### Deployment of the app to kubernetes 

- kubectl apply -f mysql.yaml
- kubectl apply -f deployment.yaml
- kubectl create namespace argocd
- kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
- kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
- kubectl port-forward svc/argocd-server -n argocd 8080:443

Login into azure first
az login --scope https://management.core.windows.net//.default

Set the cluster subscription
az account set --subscription 284adbd3-4b61-40da-b192-d55fd8ab04f8


Download cluster credentials
az aks get-credentials --resource-group rg-apparent-viper --name cluster-social-alien --overwrite-existing


Sample commands
Once you have run the command above to connect to the cluster, you can run any kubectl commands. Here are a few examples of useful commands you can try.

List all deployments in all namespaces
- kubectl get deployments --all-namespaces=true

List all deployments in a specific namespace
- kubectl get deployments --namespace <namespace-name>

List details about a specific deployment
- kubectl describe deployment <deployment-name> --namespace <namespace-name>

Get logs for all pods with a specific label
- kubectl logs -l <label-key>=<label-value>

