# demo-app-repo
ARGOCD+KARGO+CICD WITH PROPER DEPLOYMENT STRATEGY FOR DEV, STAGE AND PROD.
minikube ip : 192.168.49.2
please run "minikube tunnel" and your ingress resources would be available at "127.0.0.1"

 kubectl port-forward svc/argocd-server -n argocd 9090:443
Forwarding from 127.0.0.1:9090 -> 8080
Forwarding from [::1]:9090 -> 8080

helm install kargo oci://ghcr.io/akuity/kargo-charts/kargo --namespace kargo --create-namespace --set api.adminAccount.enabled=true --set api.adminAccount.passwordHash="$2y$10$Zrhhie4vLz5ygtVSaif6o.qN36jgs6vjtMBdM6yrU1FOeiAAMMxOm" --set api.adminAccount.tokenSigningKey="kargo-poc-signing-key-1234567890" --wait

Port 9089: ArgoCD UI (GitOps engine)
Port 3100: Argo Rollouts Dashboard (deployment strategies)
Port 9091: Kargo API (promotion management)