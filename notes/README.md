# Notes

Write hardening notes here, one markdown file per topic. A practical file name is `YYYY-MM-DD-short-topic.md`. This README is the only notes file shipped with the skeleton; your write-ups stay local until you choose to commit them.

## What a note should contain

- The file or setting you reviewed
- The secure default for that setting
- The impact of leaving the weak setting in place, in one or two sentences
- The change you made
- How you verified the change (`docker compose config`, a `docker inspect` field, an image digest, a healthcheck)

## What a note must not contain

- Exploit steps, payloads, or request sequences that trigger a flaw
- CVE reproduction procedures
- Output from attack tools
- Real credentials (obvious fake lab values only, and only if a setting cannot be described without them)

## Template

```markdown
# Title

- Date:
- Setting reviewed:
- Secure default:
- Impact of the weak setting:
- Change:
- Verification:
```

Example impact line, which is enough: "Publishing `0.0.0.0` accepts connections from every interface on the host, so another machine on the network can reach the lab port. Bind `127.0.0.1` instead."

Do not extend that kind of sentence into instructions for connecting from another machine.
