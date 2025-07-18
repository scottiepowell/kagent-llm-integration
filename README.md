# KAgent + Ollama Integration

This repository provides Kubernetes manifests and configuration to integrate [KAgent](https://kagent.dev/) with a locally hosted [Ollama](https://ollama.com/) instance. The setup enables you to run and manage LLMs (such as orca-mini and tinyllama-1.1b) on your Kubernetes cluster and interact with them via KAgent.

A complete walkthrough has been published on Medium [here](https://medium.com/@renjithvr11/integrating-kagent-and-ollama-bringing-agentic-ai-closer-to-kubernetes-995f0b1f6134)
---

## Repository Structure

- **kagent/**: KAgent Helm values and configuration manifests.
- **ollama-operator/**: CRDs and model manifests for Ollama Operator.

---

## Quick Start

### 1. Create Namespaces

```bash
kubectl create namespace ollama-apps
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
kubectl apply -f ollama-operator/models/tinyllama.yaml
kubectl apply -f ollama-operator/models/llama3.21b.yaml
```

### 4. Configure and Deploy KAgent

You can install KAgent using Helm or the CLI. See [kagent/README.md](kagent/README.md) for details.

Example with Helm:

```bash
helm install kagent-crds oci://ghcr.io/kagent-dev/kagent/helm/kagent-crds --namespace kagent --create-namespace
helm install kagent oci://ghcr.io/kagent-dev/kagent/helm/kagent --namespace kagent --values kagent/values.yaml
```

Or apply the provided manifests in `kagent/` for custom configuration.

---

## Configuration Overview

- **Ollama Models**: Defined in [ollama-operator/models/](ollama-operator/models/) (e.g., `orca-mini.yaml`, `tinyllama.yaml`).
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

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=mysticrenji/kagent-llm-integration&type=Date)](https://www.star-history.com/#mysticrenji/kagent-llm-integration&Date)
