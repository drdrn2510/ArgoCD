 Step how to install ArgoCD - With cloudShell https://shell.cloud.google.com/
 kubectl create namespace argocd
 helm repo add argocd https://argoproj.github.io/argo-helm 
 helm repo update
 helm upgrade --install -n argocd argocd argocd/argo-cd
 kubectl patch configmap argocd-cmd-params-cm -n argocd --patch '{"data":{"server.insecure":"true"}}'
 kubectl delete pod -n argocd -l app.kubernetes.io/name=argocd-server
 kubectl get all -n argocd
 kubectl get secret argocd-initial-admin-secret -n argocd -o jsonpath="{.data.password}" | base64 -d && echo ----> (copy the password)
 kubectl -n argocd port-forward svc/argocd-server 8080:80 -----------------------
 --------------------------------------
 After install open browser the login to : https://localhost:8081
 Connect via web preview in cloudshell
 User name : admin
 password : The one you copied from section 9

 Dont forget to run on cloudshell - kubectl apply -f argo-repo/argo.yaml so it will sync with argo-cd
