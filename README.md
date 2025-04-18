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
          sequin-version: "latest"
          pg-password: "sequin"
          secret-key-base: "your-secret-key-base"
          vault-key: "your-vault-key"
          config-file: "./path/to/your/config.yml"
```

## Inputs

| Input             | Description                | Required | Default                                                          |
| ----------------- | -------------------------- | -------- | ---------------------------------------------------------------- |
| `sequin-version`  | Version of Sequin to use   | Yes      | latest                                                           |
| `pg-password`     | PostgreSQL password        | Yes      | sequin                                                           |
| `secret-key-base` | Secret key base for Sequin | Yes      | wDPLYus0pvD6qJhKJICO4dauYPXfO/Yl782Zjtpew5qRBDp7CZvbWtQmY0eB13If |
| `vault-key`       | Vault key for Sequin       | Yes      | 2Sig69bIpuSm2kv0VQfDekET2qy8qUZGI8v3/h3ASiY=                     |
| `config-file`     | Path to config file        | Yes      | -                                                                |

## Services

The action sets up the following services:

- Sequin service on port 7376
- PostgreSQL 16 (Alpine) on port 7377
- Redis 7 on port 7378

## Configuration

The action requires a configuration file. Example configuration:

```yaml
account:
  name: "Playground"
users:
  - account: "Playground"
    email: "admin@sequinstream.com"
    password: "sequinpassword!"
database:
  host: localhost
  port: 5432
  name: myapp
  username: myapp
  password: myapp
  pool_size: 30
redis:
  url: redis://sequin_redis:6379
secret_key_base: wDPLYus0pvD6qJhKJICO4dauYPXfO/Yl782Zjtpew5qRBDp7CZvbWtQmY0eB13If
vault_key: 2Sig69bIpuSm2kv0VQfDekET2qy8qUZGI8v3/h3ASiY=
```

## Health Check

The action includes a health check that waits for the Sequin service to be ready. It will timeout after 30 seconds if the service doesn't become available. The health check verifies the `/health` endpoint.
