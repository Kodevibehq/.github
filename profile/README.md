# Kodevibehq

Org-level defaults for every Kodevibehq repository.

## Reusable workflows

- [`secret-scan-reusable.yml`](.github/workflows/secret-scan-reusable.yml) — gitleaks on every push to `main` and every pull request, with results piped to the Kodend "Beveiliging" dashboard via the coolify-proxy ingest route.

## Org-default config files

- [`.gitleaks.toml`](.gitleaks.toml) — the default ruleset every repo inherits when it doesn't ship its own `.gitleaks.toml`.

## How a repo opts in

Add `.github/workflows/secret-scan.yml`:

```yaml
name: Secret scan
on:
  push:
    branches: [main]
  pull_request:
jobs:
  scan:
    uses: Kodevibehq/.github/.github/workflows/secret-scan-reusable.yml@main
    secrets: inherit
```

That's it. Repos can override the ruleset by committing a local `.gitleaks.toml`, and can suppress historical findings by committing a `.gitleaks-baseline.json`.
