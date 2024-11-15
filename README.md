# Deprecation Notice
- This GitHub action is deprecated and should no longer be used for authenticating against Prefect Cloud. To authenticate against Prefect Cloud in your workflows, simply set two environment variables (`PREFECT_API_KEY` & `PREFECT_API_URL`) as described [in the docs](https://docs.prefect.io/3.0/deploy/infrastructure-concepts/deploy-ci-cd#repository-secrets).

# actions-prefect-auth

## Details

A GitHub Action for authenticating into [Prefect Cloud](https://docs.prefect.io/latest/cloud/)

## Requirements

- Access to a [Prefect Cloud Account](https://docs.prefect.io/latest/ui/cloud/#welcome-to-prefect-cloud)
- [Setup Python](https://github.com/actions/setup-python) - to install prefect & other requirements

## Inputs

| Input | Desription | Required | Default |
|-------|------------|----------|---------|
| prefect-api-key | API Key to authenticate with Prefect. | true | |
| prefect-workspace | Full handle of workspace, in format `<account_handle>/<workspace_handle>`. | true | |

## Examples

### Basic Login
Log into Prefect Cloud using stored GHA Secrets

```yaml
name: Log Into Prefect Cloud
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
        uses: PrefectHQ/actions-prefect-auth@v2
        with:
          prefect-api-key: ${{ secrets.PREFECT_API_KEY }}
          prefect-workspace: ${{ secrets.PREFECT_WORKSPACE }}
```
### Simple Prefect Deploy

Deploy a Prefect flow that doesn't have a `push` step defined in the `prefect.yaml`
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
        uses: PrefectHQ/actions-prefect-auth@v2
        with:
          prefect-api-key: ${{ secrets.PREFECT_API_KEY }}
          prefect-workspace: ${{ secrets.PREFECT_WORKSPACE }}

      - name: Run Prefect Deploy
        uses: PrefectHQ/actions-prefect-deploy@v4
        with:
          requirements-file-path: ./examples/simple/requirements.txt
          entrypoint: ./examples/simple/flow.py:call_api
          additional-args: --cron '30 19 * * 0'
```

## Terms & Conditions
See here for the Prefect's [Terms and Conditions](https://www.prefect.io/legal/terms/).
