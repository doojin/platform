# Platform

## Getting started

1. Manually install ArgoCD to your cluster:
```bash
kubectl create namespace argo-cd
helm upgrade --install argo-cd argo/argo-cd \
  --namespace argo-cd \
  --set server.service.type=NodePort \
  --set server.service.nodePortHttp=30000 \
  --set server.insecure=true
```

2. Add GitHub deployment key to the ArgoCD
```bash
ssh-keygen -t ed25519 -C "argocd-deploy-key" -f ~/.ssh/argocd_deploy_key -N ""
```

- Copy the public key: `cat ~/.ssh/argocd_deploy_key.pub`
- Add it to "Deploy keys" of this repository
- Open ArgoCD UI → Settings → Repositories
- Click "Connect Repo" → "Via SSH"
- Copy the private key: `cat ~/.ssh/argocd_deploy_key` and pass it to the "SSH Private Key Data" input

3. Initialize "App of apps"
```bash
kubectl apply -f bootstrap/root-app.yaml
```