# demo-app-repo
ARGOCD+KARGO+CICD WITH PROPER DEPLOYMENT STRATEGY FOR DEV, STAGE AND PROD.

Minikube in GitHub Codespace
kubectl port-forward svc/argocd-server -n argocd 9090:80

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.yaml

helm uninstall kargo -n kargo || true
kubectl delete ns kargo --wait=false

kubectl get ns kargo -o json \
 | jq '.spec.finalizers=[]' \
 | kubectl replace --raw "/api/v1/namespaces/kargo/finalize" -f -

helm install kargo oci://ghcr.io/akuity/kargo-charts/kargo \
  --namespace kargo \
  --create-namespace \
  --set api.tls.enabled=false \
  --set api.service.port=80 \
  --set api.adminAccount.enabled=true \
  --set api.adminAccount.passwordHash='$2y$10$Zrhhie4vLz5ygtVSaif6o.qN36jgs6vjtMBdM6yrU1FOeiAAMMxOm' \
  --set api.adminAccount.tokenSigningKey='kargo-poc-signing-key' \
  --wait

kubectl port-forward -n kargo svc/kargo-api 8081:80

kubectl get pods -n kargo


Port 9089: ArgoCD UI (GitOps engine)
Port 3100: Argo Rollouts Dashboard (deployment strategies)
Port 9091: Kargo API (promotion management)# Testing DEV deployment


sTv5qMKwBmkN8gwO

kubectl argo rollouts get rollout demo-app -n demo-dev --watch

# Start port forward
kubectl port-forward svc/argocd-server -n argocd 8080:443 > /dev/null 2>&1 &
kubectl port-forward svc/argo-rollouts-dashboard -n argo-rollouts 3100:3100 > /dev/null 2>&1 &
kubectl port-forward svc/kargo-api -n kargo 8081:80 > /dev/null 2>&1 &
<!-- kubectl port-forward svc/kargo-ui -n kargo 8082:80 > /dev/null 2>&1 & -->

test trigger dev...