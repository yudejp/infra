# k3s.yude.jp
🐙 My K3s-related resources

## Setup
1. Install ArgoCD
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

1. Integrate this repository to the cluster
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: infra
  namespace: argocd
spec:
  project: default
  destination:
    server: https://kubernetes.default.svc
  source:
    repoURL: https://github.com/yudejp/infra.git
    path: .
    targetRevision: main
    directory:
      recurse: true
  syncPolicy:
    automated: {}
    syncOptions:
    - CreateNamespace=true
```

## License
MIT License.