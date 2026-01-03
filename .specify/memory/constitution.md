<!--
Sync Impact Report

- Version change: unspecified → 1.0.0
- Modified principles:
	- [PRINCIPLE_1_NAME] → User Safety & Data Integrity (NON-NEGOTIABLE)
	- [PRINCIPLE_2_NAME] → Test-First Quality (NON-NEGOTIABLE)
	- [PRINCIPLE_3_NAME] → Performance Budget & Resource Constraints
	- [PRINCIPLE_4_NAME] → Privacy-First & Opt-In Telemetry
	- [PRINCIPLE_5_NAME] → Consistent UX & Accessibility
- Added sections: Constraints & Standards; Development Workflow & Quality Gates
- Removed sections: none
- Templates reviewed:
	- .specify/templates/plan-template.md ✅ aligned
	- .specify/templates/spec-template.md ✅ aligned
	- .specify/templates/tasks-template.md ✅ aligned
	- .specify/templates/commands/*.md ⚠ pending (directory missing)
- Follow-up TODOs:
	- TODO(RATIFICATION_DATE): original adoption date unknown — please supply
-->

# myCleaner (PC Cleaning & Optimization) Constitution

## Core Principles

### User Safety & Data Integrity (NON-NEGOTIABLE)
All actions that modify user files, the registry, or system configuration MUST include an automatic backup, a clear undo/quarantine path, and create a Windows restore point when applicable. Risky operations (registry edits, secure deletion) MUST present conservative defaults and explicit user confirmation. Rationale: safety-first prevents user harm and reduces support burden.

### Test-First Quality (NON-NEGOTIABLE)
All new features and bug fixes MUST have automated tests before implementation: 
- unit tests for core logic
- integration tests for inter-component behavior
- end-to-end tests for user flows. 

Core modules MUST maintain measurable coverage targets (e.g., critical scan/clean engines ≥80% unit coverage) and all acceptance criteria from the PRD MUST be testable and automated. Rationale: prevent regressions and ensure repeatable quality.

### Performance Budget & Resource Constraints
Every release MUST meet defined non-functional targets: 
- installer size ≤ 30MB
- idle CPU < 2% 
- typical memory footprint < 150MB 
- scanning/cleanup responsiveness: typical runs ≤2 minutes for reference hardware
- measurable boot-time improvements where applicable

Performance targets are enforced by CI benchmarks and performance tests. Rationale: product value depends on restoring performance without creating new overhead.

### Privacy-First & Opt-In Telemetry
Telemetry and analytics are DISABLED by default and require explicit, revocable user consent (opt-in). Any telemetry MUST be anonymized, GDPR-compliant, and documented. No personal data is transmitted without user approval. Rationale: privacy is core to user trust and product adoption.

### Consistent UX & Accessibility
The product MUST provide a consistent, clear, and accessible user experience: clear language for destructive actions, previews before deletion, and consistent stateful feedback (progress, results, logs). Localization framework MUST be available at launch readiness. Rationale: reduces user errors and supports broad adoption.

## Constraints & Standards

- Supported platforms: Windows 11 and Windows 10 (per PRD); compatibility practices for earlier Windows versions noted in engineering backlog.
- Technology stack guidance: desktop app using .NET (C#) or native modules (C++) for performance-sensitive components; WPF recommended for UI consistency and accessibility.
- Licensing: third-party libraries MUST be MIT/Apache-2.0/BSD compatible; GPL requires legal review and explicit approval.
- Security: secure deletion algorithms and cryptographic primitives MUST use well-vetted libraries; sensitive operations logged locally; restore/quarantine enforced.
- Performance budgets and resource constraints from the PRD are normative and MUST be validated through CI performance tests before release.

## Development Workflow & Quality Gates

- All changes MUST go through CI with the following gates: linting, unit tests, integration tests, performance benchmarks for affected modules, and security/static analysis where applicable.
- Code review: every PR requires at least one engineer and one product reviewer approval. High-risk changes (registry, deletion, driver-level code) require Tech Lead sign-off and an explicit rollback plan.
- Release gating: feature flags for major features; staged rollouts and telemetry (opt-in) for pilot cohorts; rollback capability mandatory for updates.
- Documentation: every feature MUST include a spec (using `.specify/templates/spec-template.md`), test plan, and user-facing help text. Acceptance criteria in PRD map directly to automated tests.

## Governance

Amendments: Amendments to this constitution MUST be proposed in a documented PR that includes impact analysis, migration guidance, and tests or automation changes. A MINOR version bump is required for added principles or materially expanded guidance; a MAJOR bump is required for removal or redefinition of non‑negotiable principles. Patch bumps are permitted for clarifications, typos, or non-semantic refinements.

Decision authority: Ratification or material amendment requires approval by Product Management and the Engineering Lead. Technical exceptions to non-negotiables are permitted only with documented mitigation and approval from both parties.

Versioning policy (semantic):
- MAJOR: backward-incompatible governance or principle removals/redefinitions
- MINOR: new principle/section added or material expansion
- PATCH: wording/clarifications, typo fixes, non-semantic refinements

Compliance: All PRs MUST reference relevant constitution clauses when they touch core principles (safety, testing, performance, privacy, UX). The CI pipeline SHOULD flag missing test coverage, performance regressions, and missing restore/backup steps for risky operations.

**Version**: 1.0.0 | **Last Amended**: 2026-01-01
