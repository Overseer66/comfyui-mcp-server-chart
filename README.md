# mcp-comfyui-sse

Helm chart for ComfyUI SSE MCP server.

## Configuration (values.yaml)

### Basic Settings
```yaml
replicaCount: 1
```
- `replicaCount`: Number of pod replicas to deploy

### Image Settings
```yaml
image:
  repository: overseer66/mcp-comfyui-sse
  tag: latest
  pullPolicy: Always
  # imagePullSecrets:
  #   name: pull-secret
```
- `repository`: Container image repository
- `tag`: Image tag
- `pullPolicy`: Image pull policy
- `imagePullSecrets`: Private registry authentication (optional)

### Secret Settings
```yaml
# secrets:
#   imagePullSecrets:
#     name: pull-secret
#     dockerconfigjson:
```
- `imagePullSecrets.name`: Docker registry secret name
- `imagePullSecrets.dockerconfigjson`: Base64 encoded docker authentication

### Service Settings
```yaml
service:
  type: ClusterIP
  port: 8080
```
- `type`: Service type (ClusterIP, NodePort, LoadBalancer)
- `port`: Service port

### Environment Variables
```yaml
env:
  COMFYUI_HOST: "comfyui.comfyui.svc.cluster.local"
  COMFYUI_PORT: "8188"
  RETURN_URL: "true"
  WORKFLOW_DIR: "workflows"
```
- `COMFYUI_HOST`: Host address for ComfyUI. If you're using a ComfyUI service in Kubernetes, you can set this to `comfyui.comfyui.svc.cluster.local` (for a service named "comfyui" in namespace "comfyui") to access it within the Kubernetes cluster.
- Container environment variable settings

## Usage

```bash
# Preview rendered templates
helm template release-name ./mcp-comfyui-sse

# Install
helm install release-name ./mcp-comfyui-sse

# Upgrade
helm upgrade release-name ./mcp-comfyui-sse
```

## Notes
- When using private registries, both `secrets.imagePullSecrets` and `image.imagePullSecrets` need to be configured
- Adjust environment variables according to application requirements
