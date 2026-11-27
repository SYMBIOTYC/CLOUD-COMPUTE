# Compute Federation — verified bootstrap state

## Scope
This repository defines the shared compute control-plane contracts. It is not itself a deployed scheduler or worker registry.

## Execution classes
| Class | Runtime | Trust boundary | Current evidence |
|---|---|---|---|
| Repository CI | Ephemeral GitHub-hosted Ubuntu 24.04 | Untrusted PR code; read-only repository permission | Bootstrap workflow committed; run must be inspected |
| CPU worker | Separately provisioned Linux host | Registered identity, capability allowlist, capacity lease | Not yet provisioned |
| VPS/edge | Persistent Ubuntu/Debian host | Private service identity; never execute public PR code | Not yet provisioned |

## Contracts required before production dispatch
- Versioned JobIntent/TaskRequest schema with bounded payload size.
- Worker identity, capabilities, resource limits, lease expiry, heartbeat and draining lifecycle.
- Scheduler idempotency key and durable state transition log.
- TaskResult and immutable execution receipt.
- Artifact manifest with SHA-256, size, media type and provenance.
- OIDC trust constrained to exact repository, workflow/ref and protected environment.

## Security baseline
- CI has `contents: read` only.
- No self-hosted runner is used for pull requests.
- No long-lived cloud credential is stored in this public repository.
- OIDC permissions are not granted until a concrete cloud trust policy is deployed and tested.

## Acceptance gates
1. CI run succeeds and receipt artifact is downloadable.
2. Registry integration tests cover duplicate registration, expired leases and capability mismatch.
3. Dispatcher tests cover idempotent retries, cancellation and worker loss.
4. OIDC positive and negative tests prove repository/ref restrictions.
5. Persistent worker is registered and health-checked through the approved control plane.

A successful GitHub-hosted CI run proves repository CI only. It does not prove production compute capacity.
