# Safety rules

1. Bind published ports to `127.0.0.1` only.
2. Tear down with `docker compose down -v` when finished.
3. Do not port-forward lab services to the internet.
4. Document misconfigurations and **fixes**; do not add exploit scripts.
