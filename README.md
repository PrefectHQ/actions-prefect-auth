# actions-prefect-auth

## Details

A GitHub Action for authenticating into Prefect Cloud

## Requirements

- Access to a [Prefect Cloud Account](https://docs.prefect.io/latest/ui/cloud/#welcome-to-prefect-cloud)
- [Checkout](https://github.com/actions/checkout) - to clone the repo
- [Setup Python](https://github.com/actions/setup-python) - to install prefect & other requirements

## Inputs

| Input | Desription | Required | Default |
|-------|------------|----------|---------|
| prefect-api-key | API Key to authenticate with Prefect. | true | |
| prefect-workspace | Full handle of workspace, in format `<account_handle>/<workspace_handle>`. | true | |

## Example

Log into Prefect Cloud using stored GHA Secrets

```yaml
name: Deploy a Prefect flow
on:
  push:
    branches:
      - main
jobs:
  deploy_flow:
    runs-on: ubuntu-latest
    steps:
      - uses: checkout@v3

      - uses: actions/setup-python@v4
        with:
          python-version: '3.10'
      
      - name: Prefect Auth
        uses: PrefectHQ/actions-prefect-auth@v1
        with:
          prefect-api-key: ${{ secrets.PREFECT_API_KEY }}
          prefect-workspace: ${{ secrets.PREFECT_WORKSPACE }}
```

## Terms & Conditions
See here for the Prefect's [Terms and Conditions](https://www.prefect.io/legal/terms/).
