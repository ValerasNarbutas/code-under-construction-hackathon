---
agent: 'deployer'
description: 'Deploy the spec-driven application to Azure using Azure MCP'
---

# Step 6: Deploy to Azure

Deploy your completed and tested application to Azure.

## Deployment Options

Choose the Azure service that best fits your application:

| App Type | Azure Service | Best For |
|---|---|---|
| Static frontend (React, Vue) | Azure Static Web Apps | SPAs, JAMstack |
| Full-stack (Node.js, Python) | Azure App Service | Traditional web apps |
| Containerized | Azure Container Apps | Microservices, APIs |
| API / Serverless | Azure Functions | Event-driven, lightweight APIs |

## Deployment Steps

### Option A: Azure Static Web Apps
```bash
# Build the static site
npm run build

# Deploy using Azure CLI
az staticwebapp create \
  --name <app-name> \
  --resource-group <rg-name> \
  --source ./dist \
  --location westeurope
```

### Option B: Azure App Service
```bash
# Create App Service Plan and Web App
az appservice plan create --name <plan-name> --resource-group <rg-name> --sku B1 --is-linux
az webapp create --name <app-name> --resource-group <rg-name> --plan <plan-name> --runtime "NODE:20-lts"

# Deploy code
az webapp deploy --name <app-name> --resource-group <rg-name> --src-path ./dist.zip --type zip
```

### Option C: Azure Container Apps
```bash
# Build and push container
az acr build --registry <acr-name> --image <app-name>:latest .

# Create Container App
az containerapp create \
  --name <app-name> \
  --resource-group <rg-name> \
  --image <acr-name>.azurecr.io/<app-name>:latest \
  --target-port 3000 \
  --ingress external
```

Or use the Azure MCP server through Copilot for guided deployment.

If your deployment requires Bicep infrastructure, place files in `spec-driven/infra/` with modules in `spec-driven/infra/modules/`.

## Post-Deployment Verification

- [ ] Application is accessible at the Azure URL
- [ ] All features work in the deployed environment
- [ ] Run Playwright tests against the deployed URL (update `baseURL` in config)

## Expected Output

A live application deployed to Azure with a public URL.

## Feature Expansion (Optional)

Add new features using folder-based isolation:

### Spec Kit
```bash
export SPECIFY_FEATURE="dark-mode"
/speckit.specify    # Specs scoped to dark-mode feature
/speckit.implement  # Implementation scoped to dark-mode
```

### OpenSpec
```
/opsx:propose "Add dark mode toggle with system preference detection"
/opsx:apply
```

Each new feature follows the same cycle: specify → implement → test → deploy.
