# Service stub template

Copy this folder to `services/<short-name>/` when you add a service. Rename this heading to match the folder.

Until you have a normal base image, leave the folder as this README only. Do not add application source that is vulnerable by design, exploit code, payloads, or attack instructions.

## Learning objective

<!-- Hardening topic. Example: pin the base image by digest, or run with a read-only root filesystem. -->

## Image and tag

<!-- name:tag and, when you have one, the digest. -->

## Port and bind address

<!-- 127.0.0.1:HOST:CONTAINER. Write "none" if the service publishes no port. -->

## Writable paths

<!-- None, or the exact paths plus why the process must write there. -->

## Capabilities kept

<!-- ALL dropped, then each added capability and why. -->

## How to verify the secure configuration

<!-- Commands such as docker compose config, docker inspect, or a healthcheck. Describe the expected secure result. -->

## How to stop

```bash
docker compose down -v
```
