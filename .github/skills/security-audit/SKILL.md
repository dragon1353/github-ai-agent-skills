---
name: security-audit
description: Audit an authorized repository or change for practical security weaknesses. Use for secure code review, dependency and supply-chain risk, secrets exposure, authentication and authorization flaws, unsafe input handling, data protection, and threat-focused review.
---

# Security Audit

## Boundaries

- Confirm the repository and environment are within the authorized scope.
- Prefer read-only inspection and safe local checks. Do not exploit production systems, access third-party data, or perform disruptive scanning.
- Never display full secret values. If a possible secret is found, report its location and type with the value redacted.

## Workflow

1. Map entry points, assets, trust boundaries, identities, privileged operations, data stores, external services, and deployment surfaces relevant to the request.
2. Inspect authentication, authorization, input validation, output encoding, query construction, file handling, deserialization, cryptography, logging, error handling, and secret management.
3. Review dependency manifests, lockfiles, build workflows, release provenance, and permission scopes for supply-chain risk.
4. Trace plausible attacker-controlled inputs to sensitive sinks. Confirm reachability and existing mitigations before reporting.
5. Use project-approved scanners when available, treating tool output as leads rather than confirmed vulnerabilities.
6. Rank findings by exploitability, impact, affected scope, required privileges, and confidence.
7. Recommend the smallest durable remediation and a regression test or verification method.

## Finding format

Include severity, confidence, affected file and line, attack preconditions, impact, evidence, remediation, and validation. Separate confirmed vulnerabilities from hardening suggestions and unverified scanner alerts.
