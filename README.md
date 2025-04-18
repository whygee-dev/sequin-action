# Sequin Service GitHub Action

This GitHub Action sets up a Sequin service with PostgreSQL and Redis for your workflows.

## Usage

```yaml
jobs:
  setup-sequin:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Sequin Service
        uses: ./.github/actions/sequin-action
        with:
          sequin-version: "v0.6.98"
          pg-password: "sequin"
          secret-key-base: "your-secret-key-base"
          vault-key: "your-vault-key"
          config-file: "./path/to/your/config.yml" # Optional
```

## Inputs

| Input             | Description                | Required | Default           |
| ----------------- | -------------------------- | -------- | ----------------- |
| `sequin-version`  | Version of Sequin to use   | Yes      | v0.6.98           |
| `pg-password`     | PostgreSQL password        | Yes      | sequin            |
| `secret-key-base` | Secret key base for Sequin | Yes      | random string     |
| `vault-key`       | Vault key for Sequin       | Yes      | random string     |
| `config-file`     | Path to custom config file | No       | Basic config file |

## Services

The action sets up the following services:

- Sequin service on port 7376
- PostgreSQL on port 7377
- Redis on port 7378

## Configuration

You can provide a custom configuration file by setting the `config-file` input. If not provided, a default configuration will be generated with the following structure.

## Health Check

The action includes a health check that waits for the Sequin service to be ready before proceeding. It will timeout after 5 minutes if the service doesn't become available.
