# GenAI Platform Starter Project

This project contains configurations for a lightweight GenAI platform with the following components:

- [Open WebUI](https://github.com/open-webui/open-webui) - Frontend UI for interacting with LLMs
- [LiteLLM](https://github.com/BerriAI/litellm) - LLM routing and management layer
- [n8n](https://n8n.io/) - Workflow automation
- [Langfuse](https://langfuse.com/) - LLM observability and monitoring

## Local Development with Docker Compose

### Prerequisites

- Docker and Docker Compose
- API keys for LLM providers (OpenAI, Anthropic, etc.)

### Quick Start

1. Clone this repository
2. Set up your API keys in `.env`
3. Run the stack:

```bash
docker-compose up -d
```

4. Access the interfaces:
   - Open WebUI: http://localhost:3000
   - n8n: http://localhost:5678
   - Langfuse: http://localhost:3001

## Kubernetes Deployment (Local Testing)

### Prerequisites

- Minikube, kind, or other local Kubernetes cluster
- kubectl
- Flux CLI (optional, for GitOps workflow)

### Quick Start with kubectl

1. Start your local Kubernetes cluster:

```bash
minikube start
```

2. Create the resources:

```bash
kubectl apply -k kubernetes/
```

3. Set up port-forwarding to access the services:

```bash
# OpenWebUI
kubectl port-forward -n genai-platform svc/openwebui 3000:80

# n8n
kubectl port-forward -n genai-platform svc/n8n 5678:5678

# Langfuse
kubectl port-forward -n genai-platform svc/langfuse 3001:80
```

### GitOps with Flux CD

1. Install Flux:

```bash
flux bootstrap github \
  --owner=yourusername \
  --repository=genai-platform \
  --path=flux \
  --personal
```

2. Apply the Flux configurations:

```bash
kubectl apply -f flux/source.yaml
kubectl apply -f flux/kustomization.yaml
```

## Next Steps for Learning

1. Customize the LiteLLM configuration to add more models
2. Set up workflows in n8n to automate tasks
3. Configure Langfuse to track and analyze your LLM usage
4. Explore Flux CD for GitOps-driven deployments
5. Add more components like vector databases or evaluation frameworks

## Moving to Production

For a production deployment, consider:

1. Setting up proper secrets management
2. Implementing authentication
3. Adding persistent storage
4. Configuring proper ingress with TLS
5. Setting up monitoring and alerting