# Services

Each subdirectory is a **service stub** for hardening practice: either a README-only placeholder, or a build of ordinary software used to practice image and Compose defaults.

## Rules

- No exploit code, payloads, attack scripts, or proof-of-concept exploits.
- No application source whose purpose is to demonstrate how to attack a service.
- No reproduction steps for a CVE.
- A stub README names the hardening topic, the bind address, and how to verify the secure configuration.
- Pin the base image tag. Prefer a digest pin when a stub moves beyond a local experiment.
- Do not put real secrets in a Dockerfile, an `ENV` instruction, or a committed env file.

## Current stubs

| Path | What it is |
| --- | --- |
| [`placeholder/`](placeholder/README.md) | Static nginx page. Non-root, read-only root, no added capabilities, localhost bind. Not a vulnerable application. |
| [`_stub/`](_stub/README.md) | README-only template. Copy it when you start a new service folder. |

## README headings for a new stub

- Learning objective (the hardening topic, such as image pinning or a read-only root filesystem)
- Image name and tag
- Port and bind address (`127.0.0.1` only)
- Writable paths, if any, and why they must be writable
- Capabilities kept, and why each one is required
- How to verify the secure configuration
- How to stop the service

Leave the folder as documentation until you have chosen a normal base image. Do not fill it with a deliberately vulnerable app.
