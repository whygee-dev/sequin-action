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
          config-file: "./path/to/your/sequin/config.yml"
```

## Inputs

| Input             | Description                         | Required | Default                                                          |
| ----------------- | ----------------------------------- | -------- | ---------------------------------------------------------------- |
| `sequin-version`  | Version of Sequin to use            | Yes      | latest                                                           |
| `pg-password`     | Sequin internal PostgreSQL password | Yes      | sequin                                                           |
| `secret-key-base` | Secret key base for Sequin          | Yes      | wDPLYus0pvD6qJhKJICO4dauYPXfO/Yl782Zjtpew5qRBDp7CZvbWtQmY0eB13If |
| `vault-key`       | Vault key for Sequin                | Yes      | 2Sig69bIpuSm2kv0VQfDekET2qy8qUZGI8v3/h3ASiY=                     |
| `config-file`     | Path to config file                 | Yes      | -                                                                |

## Services

The action sets up the following services:

- Sequin service on port 7376
- PostgreSQL 16 (Alpine) on port 7377 for internal Sequin use
- Redis 7 on port 7378 for internal Sequin use
