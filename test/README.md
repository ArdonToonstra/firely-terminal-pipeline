# Local Test Harness

Minimal instructions to run the composite action locally with `act`.

## Prerequisites
- Docker running
- `act` installed (https://github.com/nektos/act)
- This repository cloned with the `test/` folder committed

## Secrets
Create a file (not committed) named `.secrets` in repo root:
```
SIMPLIFIER_USERNAME=you@example.com
SIMPLIFIER_PASSWORD=yourPassword
```

## Run
PowerShell example:
```
act -W .github/workflows/local-test.yml -P ubuntu-latest=catthehacker/ubuntu:act-latest -j validate --secret-file .secrets
```

## What it does
- Copies `test/` content into workspace root
- Sets up .NET, Java, Node
- Prepares global npm dir (needed for minimal act image)
- Installs Firely Terminal & SUSHI (when enabled)
- Runs validation (.NET + Java)

## Troubleshooting
- If SUSHI install fails: ensure the prep step exists or rerun with `--pull`.
- To re-run clean: remove `.act` work directory or add `--reuse=false`.
- Add `-s SIMPLIFIER_USERNAME -s SIMPLIFIER_PASSWORD` instead of secret file if preferred.
