---
name: Audit GitHub/GitLab posture with legitify
description: >-
  Run Legit Security's open source legitify scanner against a GitHub or GitLab
  organization and produce machine-readable findings (JSON or SARIF) an agent
  can triage.
api: null
operations: []
source: https://github.com/Legit-Labs/legitify
method: searched
generated: '2026-07-19'
---

# Audit SCM posture with legitify

`legitify` is Legit Security's Apache-2.0 scanner for GitHub and GitLab
misconfigurations. Every command and flag below is taken verbatim from the
project README — nothing is inferred.

## Install

```bash
brew install legitify
# or
gh extension install legit-labs/gh-legitify && gh legitify
# or from source
git clone git@github.com:Legit-Labs/legitify.git && go run main.go analyze
```

Release binaries (which ship the built-in policies) are on
https://github.com/Legit-Labs/legitify/releases — current `v1.0.11`.

## Authenticate

Supply a GitHub or GitLab token through the environment. Never inline it into
a shell history or a prompt.

```bash
export SCM_TOKEN=<your_token>
```

## Run

```bash
legitify analyze --org <org> --output-format json --failed-only
```

Useful flags:

- `--org` — limit analysis to the named organizations.
- `--namespace` — filter by resource type: `organization`, `member`,
  `repository`, `actions`, `runner_group`.
- `--output-format` — `human-readable` (default), `json`, `sarif`.
- `--scorecard` — run OSSF Scorecard checks: `yes` / `no` / `verbose`.
- `--failed-only` — emit violations only.
- `--ignore-policies-path` — file listing policies to skip.

JSON output supports grouping schemes: `flattened`, `group-by-namespace`,
`group-by-resource`, `group-by-severity`.

## Triage

1. Run with `--output-format sarif` to feed code-scanning surfaces, or `json`
   with `group-by-severity` to rank findings.
2. Re-run with `--namespace repository` to scope down noisy organizations.
3. Record accepted risks in an ignore file and pass it via
   `--ignore-policies-path` so the run stays clean and reviewable.

## Supported SCMs

GitHub Cloud, GitHub Enterprise Server, GitLab Cloud, GitLab Server.
