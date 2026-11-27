# CLOUD-COMPUTE

Control-plane contracts and scheduling for Symbiotyc Compute Federation.

## Execution classes

- **Linux CI:** ephemeral GitHub-hosted Ubuntu 24.04 runners for repository checks.
- **CPU workers:** separately managed compute workers with explicit capabilities, capacity, leases, isolation, and provenance.
- **VPS:** persistent Ubuntu/Debian hosts for approved edge services. Public pull-request jobs must never run on these hosts.

## Security and delivery

Use least-privilege GitHub Actions permissions. Cloud access must use short-lived OIDC federation with repository and protected-ref restrictions; do not store service-account keys. Validate job payloads, enforce limits and idempotency, and record immutable execution receipts and artifact checksums.

## Bootstrap CI status

The initial Linux CI checks the README baseline on GitHub-hosted `ubuntu-24.04` and publishes a 14-day `ci-receipt.json` artifact. A passing bootstrap run proves only that the hosted CI job ran; it does not prove that a Worker Registry, dispatcher, cloud trust, or persistent worker is deployed.

This repository describes architecture and bootstrap contracts. Require successful service-specific checks and a verified execution receipt before marking a phase complete.
