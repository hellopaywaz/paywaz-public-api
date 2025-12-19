# Repository Health Report

**Overall score:** 50/100 — OpenAPI spec is lintable with reproducible commands, but quality gates and release/ops practices are still early-stage.

## Score breakdown
- **CI/Build Reproducibility (25): 18/25** — CI now installs Node 20, runs lint/tests, and bundles the spec; scripts are pinned to Redocly 1.29.0 via `npx`. Package-lock exists but no vendored dependencies due to proxy restrictions.
- **Tests/Quality Gates (20): 8/20** — Only schema linting exists; there are no contract tests, SDK samples, or negative-case checks.
- **Security Baseline (20): 10/20** — SECURITY.md exists and CI uses least-privilege actions, but there is no automated dependency/security update service or secret-scanning workflow.
- **Release/Packaging (15): 5/15** — No tagged releases, changelog, or published bundles. Build outputs a bundled spec but it is not versioned or attached to releases.
- **Documentation/Onboarding (10): 7/10** — README documents golden commands and setup; additional docs exist for auth/webhooks. Missing quickstart and contribution workflow for specs.
- **Ops/Runbooks/Observability (10): 2/10** — No health checks, SLIs/SLOs, or operational playbooks (service not yet live).

## P0 blockers (must-fix)
None identified after this pass.

## P1 risks (should fix soon)
- Lack of automated dependency/security updates (e.g., Dependabot) and secret scanning leaves tooling drift unchecked.
- No contract or integration tests for the OpenAPI spec; only linting runs in CI.
- No tagged releases or changelog to track spec changes for consumers.
- `npx` downloads of Redocly require external network access; environments without registry access cannot run the golden commands.

## P2 hygiene (nice-to-have)
- Expand documentation with a quickstart that demonstrates sample requests and expected responses.
- Add example payload fixtures and negative-case schemas for better consumer guidance.
- Consider attaching bundled artifacts to releases once tagging is in place.

## CI status
- **docs-ci.yml** — placeholder docs check (echo).
- **openapi-lint.yml** — runs `npm run lint` (Redocly lint) on PRs/pushes touching OpenAPI/tooling files.
- **openapi-validate.yml** — installs Node 20, runs `npm test`, and builds the bundled OpenAPI artifact with `npm run build`.

## Security baseline
- SECURITY.md present with contact path; no SECURITY advisories or scanner pipelines.
- GitHub Actions use `actions/checkout@v4` and `actions/setup-node@v4` without elevated permissions.
- No dependency update automation or secret-scanning workflow configured.

## Release readiness
- Package version is `0.1.0`; no tags/releases or changelog. Build script outputs `dist/openapi.bundle.yaml` but it is not published.
- No release checklist or artifact promotion path.

## Ops readiness
- No runtime service yet; no health checks, monitoring, or incident/runbook documentation for when APIs go live.

## Repo hygiene
- Baseline files now present: README, LICENSE (points to Paywaz proprietary terms), SECURITY.md, CONTRIBUTING.md, CODE_OF_CONDUCT.md, CODEOWNERS, .editorconfig, .gitignore.
- Documentation lives under `docs/` and `openapi/`; redocly configuration is in `redocly.yaml`.
