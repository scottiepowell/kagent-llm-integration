# Create Namespace

```bash
kubectl create namespace ollama-apps
kubectl create namespace litellm-gateway
kubectl create namespace kagent
```

# 1. Install Ollama CRDs
```bash
kubectl apply --server-side=true -f https://raw.githubusercontent.com/nekomeowww/ollama-operator/v0.10.1/dist/install.yaml
```