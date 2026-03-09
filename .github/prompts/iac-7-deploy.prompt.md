---
agent: 'deployer'
description: 'Deploy the complete infrastructure solution to Azure — create resource group, run deployment, verify resources'
---

# Step 7: Deploy to Azure

Deploy the complete infrastructure solution to Azure.

## Deployment Steps

1. **Authenticate** — Verify Azure CLI login and correct subscription
2. **Create Resource Group** — `rg-todo-dev-westeurope` in West Europe
3. **What-If Preview** — Run what-if deployment to review changes
4. **Deploy** — Execute the Bicep deployment
5. **Verify** — Confirm all resources are created and healthy
6. **Output** — Display Web App URL, resource list, and deployment status

## Configuration

- **Resource Group**: `rg-todo-dev-westeurope`
- **Location**: `westeurope`
- **Template**: `infra/main.bicep`
- **Parameters**: `infra/main.bicepparam`

## Verification Checklist

After deployment, verify:
- [ ] Web App is running and accessible
- [ ] SQL Server has public access disabled
- [ ] Private endpoint is connected and approved
- [ ] NSG rules are applied to subnets
- [ ] Managed identity is assigned to Web App
- [ ] All resources have required tags
