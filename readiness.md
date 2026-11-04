# Beacon release review

## Pipeline audit
Gap / risk / repaired dependency:
Production reviewer control to configure (not demonstrated locally):
Secret handling and scope:

## Traceability
Why PATCH is appropriate:
Candidate image and annotated Git tag:
Record tag -> code commit in PDF using git rev-parse commands.
Image-tag mutability limitation:

## Incident recovery
Evidence and rollback vs forward decision:
Known-good target:
Proposed kubectl command (not executed):
Recovery checks after action:

## Release note and decision
Change scope:
Local validation proof:
Open risk / owner / mitigation:
Current production decision and blocker:
Terraform vs Kubernetes responsibilities:

## Beacon release review

Gap/risk/repaired dependency: Production could run without validation passing; added `needs: validate`.
Production reviewer control to configure (not demonstrated locally): Required reviewers in Github Settings > Environments > production.
Secret handling and scope: Secret referenced only via `secrets.REGISTRY_TOKEN`, scoped to production, never printed.

## Trceability
Why PATCH is appropriate: Backward-compatible bug fix.
Candidate image and annotated Git tag: beacon-service:v2.3.1; annotated tag v2.3.1 on final commit.

## Incident recovery
Evidence and rollback vs forward decision: Suppied fixture; 35% failutres, rising, root cause unknownl rollback.
Known-good target: beacon-service:v2.3.0
Proposed kubectl command: `kubectl set image deployment/beacon beacon=beacon-service:v2.3.0`
Recovery checks after action: Rollback status, error rate normal, readiness passing, image is v2.3.0

## Release note and decision
Change scope: Workflow need, deployment image, rollback target.
Local validation proof: unittest passes; check_release.py shows 3 PASS.
Open risk/owner/migration: Reviewers not configured; owner Aryan; configure reviewers and pin digest.
Current production decision and blocker: NO-GO; approval not REQUESTED, NOT DEPLOYED.
Terraform vs Kubernetes responsibilities: Terraform provisions infrastructure; Kubernetes operates workloads.