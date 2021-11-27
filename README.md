## Argo CD can be installed using the below commands
# Step 1
This will create a new namespace, argocd, where Argo CD services and application resources will live.

kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# Step 2
By default, the Argo CD API server can be accessed from an external IP. To access the API server, change the argocd-server service type to LoadBalancer

kubectl patch svc argocd-server -n argocd -p ‘{“spec”: {“type”: “LoadBalancer”}}’

# note it's not working then go in argocd namsepace and edit service and in end of the file cahnge Typ: LoadBalancer

 kubectl edit service/argocd-server -n argocd

# to see which port is open to access this app use 

kubectl get svc -n argocd 


# Step 3
Access the Argo CD external UI via your default browser window and login by visiting the IP/hostname:service_port. The Admin account password is auto-generated and stored in a secret named argocd-initial-admin-secret in your Argo CD installation namespace. This initial password is stored as clear text in the field password in the secret mentioned above and is retrieved using kubectl

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath=“{.data.password}” | base64 -D

# this cmd not work get seret output in json than get password and the go to https://www.base64decode.org/  and decode it 

kubectl -n argocd get secret argocd-initial-admin-secret -o json
