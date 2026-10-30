# placeholder

Static file stub for the root Compose example. It is **not** a vulnerable application and it does not demonstrate an attack.

## Learning objective

Practice a localhost port bind, a read-only container root, dropped capabilities, and a clean teardown. The page content is a single HTML file.

## Image

- Base: `nginx:1.27-alpine` pinned by digest in the Dockerfile
- Local tag applied by Compose: `docker-hardening-lab-placeholder:local`
- Process user: `nginx` (set in the Dockerfile)
- Listens on container port 8080, published as `127.0.0.1:8080` on the host
- The upstream image metadata still records `EXPOSE 80`. That port is not published. `docker compose port` should show only `127.0.0.1:8080`.
- The official nginx entrypoint is not used. `start-nginx.sh` only creates temp directories under `/tmp` and execs nginx.

## Writable paths

The root filesystem is read-only. Compose mounts one tmpfs:

- `/tmp` (`nosuid`, `nodev`, `noexec`, 16m)

The pid file and nginx client/proxy temp directories live under `/tmp/nginx`.

## Capabilities

`cap_drop: [ALL]` with nothing added back. Port 8080 does not need `NET_BIND_SERVICE`.

## Verify

From the repository root, after `docker compose up --build`:

```bash
docker compose port placeholder 8080
curl -fsS http://127.0.0.1:8080/
docker inspect --format '{{.HostConfig.Privileged}} {{.HostConfig.ReadonlyRootfs}} {{.HostConfig.CapDrop}}' \
  "$(docker compose ps -q placeholder)"
```

Expect the published address to be `127.0.0.1:8080`, `Privileged` to be `false`, `ReadonlyRootfs` to be `true`, and `CapDrop` to include `ALL`.

## Stop

```bash
docker compose down -v
```
