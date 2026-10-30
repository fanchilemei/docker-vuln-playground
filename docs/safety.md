# Safety rules

Short form for anyone cloning this repository. The full ban on exploit material is in the root README. Review lists are in [`checklists/README.md`](../checklists/README.md).

1. Bind published ports to `127.0.0.1` only.
2. Tear down with `docker compose down -v` when finished.
3. Do not port-forward lab services to the internet, and do not run them on a public cloud IP.
4. Do not mount the Docker socket into a lab container.
5. Document misconfigurations and **fixes**. Do not add exploit scripts, payloads, or reproduction steps.
6. This tree is a hardening skeleton. Do not add intentionally vulnerable application source.
