# KAgent + Ollama Integration

This repository provides Kubernetes manifests and configuration to integrate [KAgent](https://kagent.dev/) with a locally hosted [Ollama](https://ollama.com/) instance. The setup enables you to run and manage LLMs (such as orca-mini and hermes-2-pro-llama-3-8b) on your Kubernetes cluster and interact with them via KAgent.

---

## Repository Structure

- **kagent/**: KAgent Helm values and configuration manifests.
- **litellm/**: LiteLLM deployment and configuration.
- **ollama-operator/**: CRDs and model manifests for Ollama Operator.

---

## Quick Start

### 1. Create Namespaces

```bash
kubectl create namespace ollama-apps
kubectl create namespace litellm-gateway
kubectl create namespace kagent
```

### 2. Install Ollama Operator CRDs

```bash
kubectl apply --server-side=true -f https://raw.githubusercontent.com/nekomeowww/ollama-operator/v0.10.1/dist/install.yaml
```

### 3. Deploy Ollama Models

Apply the model manifests for Ollama:

```bash
kubectl apply -f ollama-operator/models/orca-mini.yaml
kubectl apply -f ollama-operator/models/hermes2.yaml
```

### 4. Configure and Deploy KAgent

You can install KAgent using Helm or the CLI. See [kagent/README.md](kagent/README.md) for details.

Example with Helm:

```bash
helm install kagent-crds oci://ghcr.io/kagent-dev/kagent/helm/kagent-crds --namespace kagent --create-namespace
helm install kagent oci://ghcr.io/kagent-dev/kagent/helm/kagent --namespace kagent --values values.yaml
```

Or apply the provided manifests in `kagent/` for custom configuration.

---

## Configuration Overview

- **Ollama Models**: Defined in [ollama-operator/models/](ollama-operator/models/) (e.g., `orca-mini.yaml`, `hermes2.yaml`).
- **KAgent**: Values and model config in `kagent/values.yaml` and `kagent/llama3.2-config.yaml`. Example agent in `kagent/kagent-agent.yaml`.

---

## References

- [KAgent Documentation](https://kagent.dev/docs/)
- [Ollama Operator](https://github.com/nekomeowww/ollama-operator)
- [LiteLLM Docs](https://docs.litellm.ai/docs/)
- [Ollama Supported Models](https://docs.litellm.ai/docs/providers/ollama)

---

## License

See [LICENSE](LICENSE).
