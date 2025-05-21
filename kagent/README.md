# CLI Option
```bash
export OPENAI_API_KEY="your-api-key-here"
# Download/run the install script
curl https://raw.githubusercontent.com/kagent-dev/kagent/refs/heads/main/scripts/get-kagent | bash
kagent install
```
# Helm option
```bash
helm install kagent-crds oci://ghcr.io/kagent-dev/kagent/helm/kagent-crds \
 --namespace kagent --create-namespace

export OPENAI_API_KEY="your-openai-api-key"
export KAGENT_DEFAULT_MODEL_PROVIDER=ollama

helm install kagent oci://ghcr.io/kagent-dev/kagent/helm/kagent \
 --namespace kagent \
 --set providers.default="ollama"
 ```