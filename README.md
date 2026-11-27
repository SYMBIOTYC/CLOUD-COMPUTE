# CLOUD-COMPUTE

Control-plane contracts and scheduling for Symbiotyc Compute Federation.

## Execution classes
- **Linux CI:** ephemeral GitHub-hosted Ubuntu 24.04 runners for repository checks.
- **CPU workers:** separately managed compute workers with explicit capabilities, capacity, leases, isolation, and provenance.
- **VPS:** persistent Ubuntu/Debian hosts for approved edge services. Public pull-request jobs must never run on these hosts.

## Security and delivery
Use least-privilege GitHub Actions permissions. Cloud access must use short-lived OIDC federation with repository and protected-ref restrictions; do not store service-account keys. Validate job payloads, enforce limits and idempotency, and record immutable execution receipts and artifact checksums.

This repository describes architecture and bootstrap contracts. A README or workflow does not prove that a registry, dispatcher, cloud trust, or persistent worker is deployed. Require successful run/deployment evidence before marking a phase complete.

## Documentation

[Architecture and acceptance](docs/architecture-and-acceptance.md)
