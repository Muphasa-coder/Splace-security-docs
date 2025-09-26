# Secure SDLC (SPLACE) — [SPLACE MARKET PLACE]

## Purpose
Define required security gates, PR checks, test-data rules and release sign-off for this repo. This document implements the Secure SDLC phase for SPLACE MARKET PLACE.

## Inputs
- Threat model: `threat-model/` (assets, DFDs, entry points)
- Tech stack: (list languages, frameworks)
- Deployment targets: (staging URL(s), cloud accounts)

## Security gates (required on PR)
1. SCA (dependency) scan — job name: `dependency-scan`
2. SAST — job name: `sast`
3. Secrets scanning — job name: `secrets-scan`
4. IaC scanning (Terraform/CloudFormation) — job name: `iac-scan`
5. Container image scan (if repo builds images) — job name: `container-scan`
6. DAST on staging — job name: `dast-staging` (run after a staging deploy or via workflow_dispatch)

> All jobs must return non-error or a documented exception/allowlist PR before merge.

## Pull-request checks & review
- Minimum reviewers: **2** (including one from security or code-owner).
- Required checklist (PR template must include).
- Severity SLAs (suggested — adapt to org): Critical / High / Medium / Low — triage & fix targets are maintained by Security Ops (document below).

## Branch protection
Protect `main` (or `master`) with:
- Require pull request reviews (minimum 2)
- Require status checks to pass — list CI checks above
- Require signed commits (optional)
- Include administrators (optional)

## Security test data policy (summary)
- Never use raw production PII in test fixtures.
- Use synthetic or anonymized data. Storage in test environments must be encrypted.
- Secrets for test environments kept in the org secret manager with least privilege.
- Logs in test env must be redacted of PII.

(Full policy at `SECURITY_TEST_DATA_POLICY.md`)

## Release sign-off
- Release owner (Dev lead) + Security approver must sign-off before release to production.
- Release checklist must include: threat model references, outstanding high/critical vulnerabilities (link to issues), secrets review, infra-change review.

## Roles & responsibilities
- Dev owner: implement CI stubs, respond to triage.
- Security owner: review PRs flagged by SAST and triage findings.
- Release owner: coordinate sign-off.

## Implementation (CI job names)
- dependency-scan
- sast
- secrets-scan
- iac-scan
- container-scan
- dast-staging

## Done criteria
- `Secure-SDLC.md` committed to repo.
- PR template added and enforced.
- Each required CI job exists (stubs ok) and appears as a status check.
- Branch protection requires those status checks and 2 reviewers.
- `SECURITY_TEST_DATA_POLICY.md` and `RELEASE_SIGNOFF.md` committed.

