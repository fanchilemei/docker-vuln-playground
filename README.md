# docker-vuln-playground

Local Docker playground of **intentionally weak mini-services** for learning how misconfigurations and outdated stacks look from a **defender’s** point of view.

Services are meant to run on **localhost only**. This repo starts as a skeleton; concrete service definitions can be added later.

**Do not** add working exploit code, attack scripts, or public-facing deployments.

## Overview

- Goal: practice recognizing insecure defaults, reading configs, and applying fixes in a disposable lab.
- Scope: small Docker Compose (or similar) services under your control.
- Non-goals: CTF challenge packs that teach exploitation chains, remote attack tooling, or cloud-exposed vulnerable hosts.

## Safety rules (required)

1. **Never expose** these services on a public IP, cloud VM, or open port-forward. Bind to `127.0.0.1` only.
2. Use an isolated Docker network; tear down stacks when finished (`docker compose down -v`).
3. Do not point scanners or attack tools at anything outside this lab.
4. Do not commit real credentials; use obvious lab-only placeholders.
5. If a service is “vulnerable by design,” document the **misconfiguration and the fix**, not how to exploit it.

## Suggested structure

```text
services/      # One folder per mini-service (Dockerfile, compose snippets, config)
docs/          # Threat model notes, hardening checklists, lesson write-ups
```

Starter note: `services/` and `docs/` will be populated later. Until then, this README is the contract for how new material should be added.

## Adding a service later

When you add a service, include:

- What learning objective it serves (e.g. “weak file permissions”, “outdated base image”).
- Exact localhost ports and bind address.
- How to start and stop it safely.
- How to **verify the fix** (config change, image bump, healthcheck)—not an exploit path.

## Disclaimer

Educational and defensive practice only. You are responsible for keeping lab traffic on your machine and for not attacking third-party systems.

## License

Add a license when you publish reusable compose files.
