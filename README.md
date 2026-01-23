# demo-app-repo
ARGOCD+KARGO+CICD WITH PROPER DEPLOYMENT STRATEGY FOR DEV, STAGE AND PROD.

Minikube in GitHub Codespace
kubectl port-forward svc/argocd-server -n argocd 9090:80

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.yaml

helm install kargo oci://ghcr.io/akuity/kargo-charts/kargo \
  --namespace kargo \
  --create-namespace \
  --set api.adminAccount.enabled=true \
  --set api.adminAccount.passwordHash='$2y$10$Zrhhie4vLz5ygtVSaif6o.qN36jgs6vjtMBdM6yrU1FOeiAAMMxOm' \
  --set api.adminAccount.tokenSigningKey='kargo-poc-signing-key' \
  --set api.auth.enabled=true \
  --wait

kubectl get pods -n kargo


Port 9089: ArgoCD UI (GitOps engine)
Port 3100: Argo Rollouts Dashboard (deployment strategies)
Port 9091: Kargo API (promotion management)# Testing DEV deployment


sTv5qMKwBmkN8gwO