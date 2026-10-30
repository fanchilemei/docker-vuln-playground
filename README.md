# docker-vuln-playground

Local skeleton for **Docker security learning and hardening practice**.

The repository name is historical. Everything in this tree is **defensive scaffolding**: a secure-by-default Compose stub, empty service folders, note templates, and checklists. It is not a set of vulnerable applications, and it is not a place to practice attacks.

## Explicit ban

Do not add any of the following to this repository:

- Exploit code, proof-of-concept exploits, payloads, shells, or attack scripts
- Intentionally vulnerable application source whose purpose is to show how to attack a service
- Step-by-step reproduction procedures for CVEs or for misconfiguration attacks
- Scanner configs, wordlists, or other tooling aimed at breaking into this lab or any other system
- Instructions for exposing the lab on a public IP, a cloud VM, or an open port-forward

You may add empty service stubs, Compose examples that follow secure defaults, hardening checklists, and short notes. A note may name a weak setting, state the impact in a sentence or two, and describe the **fix** plus how to confirm it from configuration (`docker compose config`, `docker inspect`, image tag or digest, healthcheck). It must not describe how to attack that setting.

## What to practice

- Read a Compose file for insecure defaults: publishing on all interfaces, `privileged`, host networking, a mounted Docker socket, missing user or capability limits, unpinned images.
- Apply the secure defaults in `checklists/`.
- Record what you changed under `notes/`, including the command you used to verify the fix.

## Layout

```text
compose/       How the example Compose file is structured and which defaults it sets
services/      One folder per service stub (no vulnerable applications)
notes/         Hardening notes (template in the folder README)
checklists/    Review lists for a lab session
docs/          Short safety rules for anyone who clones the repo
docker-compose.yml   Minimal localhost-only placeholder stack
```

## Example stack

The root `docker-compose.yml` is a **placeholder stub**. It builds `services/placeholder`, which serves one static HTML page with nginx. That page is not a vulnerable application. The published port is bound to `127.0.0.1` only.

From the repository root:

```bash
docker compose config
docker compose up --build
curl -fsS http://127.0.0.1:8080/
docker compose down -v
```

`docker compose config` prints the resolved file so you can review binds and mounts before any container starts. Tear the stack down when you finish, including anonymous volumes (`-v`).

Details of the secure defaults on that file are in `compose/README.md`.

## Safety rules

1. Bind every published port to `127.0.0.1`. Do not publish on `0.0.0.0` or on a routable address.
2. Keep services on a user-defined bridge network. Do not set `network_mode: host` or `pid: host`.
3. Do not mount `/var/run/docker.sock` or broad host paths into a service.
4. Do not commit real credentials. If a stub needs a placeholder value, make it obviously fake and local.
5. Do not point tools at any system outside this lab.

## Adding a service later

Follow `services/README.md`. New folders start as documentation stubs. Application files, when you add them, must be ordinary software used to practice configuration — not a target with a known attack path.

## Disclaimer

Educational hardening practice on machines you control. You are responsible for keeping lab traffic on your own computer and for not attacking anyone else's systems.

## License

Add a license before treating these Compose files as reusable outside this repository.
