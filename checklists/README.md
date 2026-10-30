# Hardening checklists

Use these lists when you review the example stack or a stub you add later. Each item is a configuration check or a fix. This page does not describe how to attack a weak setting.

If a box fails, record the setting and the fix under `notes/`. State the impact in a sentence. Do not write an exploit, a payload, or a reproduction procedure.

## Before you start

- [ ] You are on a machine you control, and you intend to bind only to `127.0.0.1`.
- [ ] No Compose override file publishes a port on `0.0.0.0` or mounts the Docker socket.
- [ ] `docker compose config` succeeds, and the resolved file matches what you expect to run.
- [ ] The project contains no exploit code, payloads, or intentionally vulnerable application source.

## Compose service review

- [ ] Every published port uses a `127.0.0.1` host address.
- [ ] `restart` is `"no"`, or you have written down why it is not.
- [ ] `privileged` is unset or false.
- [ ] `network_mode: host` and `pid: host` are absent.
- [ ] No volume mounts `/var/run/docker.sock`.
- [ ] No volume mounts a broad host path such as `/`, `/var/run`, or your home directory.
- [ ] `security_opt` includes `no-new-privileges:true`.
- [ ] Capabilities start from `cap_drop: [ALL]`. Each `cap_add` entry has a one-line reason in the service README.
- [ ] The service does not use the default Compose network when a named network is enough.
- [ ] Memory and pid limits are set.
- [ ] `read_only: true` is set, or the service README explains the paths that must stay writable and mounts only those paths.

## Image and build review

- [ ] The base image tag is pinned. A digest pin is recorded when the stub is kept.
- [ ] The Dockerfile does not contain real secrets in `ENV`, `ARG`, or copied files.
- [ ] The image runs a normal upstream or distro package, not an application added so it can be attacked.
- [ ] A `.dockerignore` excludes `.git`, `.env`, and local notes if the build context could pick them up.

## Runtime review

- [ ] `docker inspect` shows `Privileged=false` and the read-only flag you configured.
- [ ] `docker compose port` prints `127.0.0.1`, not `0.0.0.0`.
- [ ] The container is not attached to the host network.
- [ ] A localhost request, if the stub serves one, returns the placeholder page and nothing else.

## After the session

- [ ] `docker compose down -v` has removed the project containers and anonymous volumes.
- [ ] You did not leave a port-forward, a reverse tunnel, or a cloud security-group rule aimed at the lab.
- [ ] Any note you commit follows `notes/README.md` and stays inside the ban in the root README.

## Banned content (do not merge)

- Exploit proof-of-concept code, payloads, webshells, or attack scripts
- Vulnerable application source added to demonstrate an attack
- CVE reproduction steps, including "authorized" or fictional framings of those steps
- Commits of real credentials or of a live kubeconfig, cloud key, or SSH private key
