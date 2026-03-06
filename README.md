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
        id: setup-sequin
        uses: whygee-dev/sequin-action
        with:
          sequin-version: "v0.14.6"
          config-file: "./path/to/your/sequin/config.yml"
          # Optional: override the auto-selected metrics port if needed.
          metrics-port: "18376"

      - name: Print selected metrics port
        run: echo "Sequin metrics port is ${{ steps.setup-sequin.outputs.metrics-port }}"
```

## Inputs

| Input             | Description                         | Required | Default                                                          |
| ----------------- | ----------------------------------- | -------- | ---------------------------------------------------------------- |
| `sequin-version`  | Version of Sequin to use            | Yes      | v0.14.6                                                          |
| `pg-password`     | Sequin internal PostgreSQL password | Yes      | sequin                                                           |
| `secret-key-base` | Secret key base for Sequin          | Yes      | wDPLYus0pvD6qJhKJICO4dauYPXfO/Yl782Zjtpew5qRBDp7CZvbWtQmY0eB13If |
| `vault-key`       | Vault key for Sequin                | Yes      | 2Sig69bIpuSm2kv0VQfDekET2qy8qUZGI8v3/h3ASiY=                     |
| `config-file`     | Path to config file                 | Yes      | -                                                                |
| `health-check-timeout` | Timeout in seconds for the health check | No | 30 |
| `metrics-port`    | Sequin metrics port. Leave unset to auto-select the first free port from `8376`, `18376`, `28376`, `38376`, `48376`. | No | auto |
| `docker-hub-username` | Docker Hub username for authentication | No | - |
| `docker-hub-password` | Docker Hub password or PAT for authentication | No | - |

## Outputs

| Output | Description |
| ------ | ----------- |
| `metrics-port` | The metrics port selected by the action, whether auto-selected or explicitly provided. |

## Services

The action sets up the following services:

- Sequin service on port 7376
- PostgreSQL 16 (Alpine) on port 7377 for internal Sequin use
- Redis 7 on port 7378 for internal Sequin use
- Sequin metrics on an auto-selected host port unless `metrics-port` is provided
