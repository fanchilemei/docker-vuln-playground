# Compose

The runnable example is [`docker-compose.yml`](../docker-compose.yml) at the repository root, so `docker compose` works without a `-f` flag. This folder explains that file. Do not add a second stack that runs vulnerable software, exploit helpers, or intentionally weak applications.

## What the example is

A single service, `placeholder`, built from `services/placeholder`. The image serves one static HTML file with nginx. It exists so you can practice reading a Compose file, binding a port to loopback, and tearing a project down. It is not a vulnerable target.

## Secure defaults on the example

| Setting | Role |
| --- | --- |
| `127.0.0.1:8080:8080` | The host port accepts connections only from this machine. The container listens on 8080 as a non-root user. |
| `restart: "no"` | The lab does not come back after a reboot or a daemon restart. |
| `read_only: true` | The container root filesystem cannot be modified. |
| `tmpfs` on `/tmp` | The only writable path. It is size-capped, `noexec`, and `nosuid`. The start script creates nginx temp directories there. |
| `no-new-privileges:true` | A process cannot gain privileges through setuid files. |
| `cap_drop: [ALL]` and no `cap_add` | The process does not bind a privileged port and does not need extra capabilities. |
| `pids_limit`, `mem_limit`, `cpus` | A runaway process in this stub stays small. |
| User-defined `lab` network | The service is not attached to the default network and does not use host networking. |
| `lab.vulnerable: "false"` | Label so a later review can see this project does not claim to be a vulnerable app. |

`network_mode: host`, `privileged: true`, `pid: host`, and a mount of `/var/run/docker.sock` are absent on purpose. Leave them absent.

The `lab` network is a normal bridge so the published loopback port keeps working on common Docker engines. An `internal: true` network is a stronger isolation choice when a service does not need a published port. If you turn it on, confirm with `docker compose config` and a local request that the engine still maps `127.0.0.1` the way you expect.

## Commands

Run these from the repository root:

```bash
docker compose config
docker compose up --build
curl -fsS http://127.0.0.1:8080/
docker compose down -v
```

## Local overrides

Docker Compose automatically merges `compose.override.yml` and `docker-compose.override.yml` when they sit next to the main file. Those names are gitignored so a personal override (for example a different host port) is not committed. Do not use an override to publish on `0.0.0.0` or to turn this stub into an attack target.

## Adding another service

1. Create `services/<name>/` from the template in `services/_stub/README.md`.
2. Add the service to the root Compose file with the same class of defaults: loopback bind, `restart: "no"`, `no-new-privileges`, dropped capabilities, read-only root where the process allows it, and resource limits.
3. Document any capability you add back, and why that process needs it.
4. Update `services/README.md` with one row for the new stub.

## Out of scope

Attack reproductions, exploit containers, and images chosen because they are vulnerable do not belong here. The ban is in the root README.
