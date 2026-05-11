# .github

Organization-wide GitHub configurations and reusable workflows.

## Reusable Workflows

### Terraform/CDKTF Cost Analysis

Automated cost analysis for Terraform and CDKTF PRs using Azure-native tools + GitHub Copilot.

**Usage in any repository:**

```yaml
name: Terraform/CDKTF Cost Analysis

on:
  pull_request:
    paths:
      - '**/*.tf'
      - '**/*.tfvars'
      - '**/*.ts'
      - '**/cdk.json'
      - '**/cdktf.json'

jobs:
  cost-analysis:
    uses: sabihsaleh/.github/.github/workflows/terraform-cost-analysis-reusable.yml@main
    with:
      terraform_directory: 'infra'
      iac_framework: 'auto' # auto | terraform | cdktf
      cdk_synth_command: 'npx cdktf synth --output .cost-analysis/generated-tf'
    secrets:
      AZURE_CLIENT_ID: ${{ secrets.AZURE_CLIENT_ID }}
      AZURE_TENANT_ID: ${{ secrets.AZURE_TENANT_ID }}
      AZURE_SUBSCRIPTION_ID: ${{ secrets.AZURE_SUBSCRIPTION_ID }}
    permissions:
      contents: read
      pull-requests: write
      id-token: write
      models: read
```

## Features

- 🤖 AI-powered analysis using GitHub Copilot
- 🔵 Azure-native data (Resource Graph, Advisor, Cost Management)
- 🧱 Supports Terraform and CDKTF (auto-detect + synth)
- 🏷️ Tag validation
- 🗑️ Orphaned resource detection
- 💬 Automated PR comments
