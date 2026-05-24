# DevSecOps Gates

**Output:** `devsecops-gates.png` (alongside this file)
**Aspect:** 16:9
**Approved version:** v0.1

Transversal view: which security controls apply at each stage of the lifecycle, from a developer's commit to ongoing operations. Companion to `ci-pipeline.png` and the GitOps loop diagrams. Chips with stronger magenta borders are controls **already shipped** by `AItizate/gh-actions-templates` or `AItizate/forjate`; the rest are recommendations.

## Command (v0.1 — final)

```bash
gemini -y -p '/generate "DevSecOps gates diagram showing which security controls apply at each stage of the lifecycle, from a developer commit to ongoing operations. Horizontal stages with stacked control chips under each one. Single 16:9 wide cinematic frame. Cyberpunk dystopian terminal aesthetic — dark deep-navy background #0A1428 with very subtle horizontal scanlines and faint grain noise. Cyan #5BB4FF primary accents, occasional magenta #FF5BBF and warm amber #FFB45B highlights on key labels. Monospace terminal-style font for chip labels, slightly bolder geometric sans for section titles. Slightly imperfect borders with subtle 1-2px chromatic drift on a few boxes. NO PHOTOS NO 3D NO LOGOS NO COMPANY NAMES NO WATERMARK.

CRITICAL: do NOT render any of these words anywhere in the image: LEFT, RIGHT, CENTER, COLUMN, SECTION, ROW, LAYOUT, AREA, UPPER, LOWER, TOP, BOTTOM, GROUP, PANEL, STAGE. Only render actual content labels.

LAYOUT (instructions for you only, do not write these on the image):

Across the upper part of the image, a horizontal flow of 6 wide rounded rectangles arranged side by side, separated by thin cyan arrows pointing from one to the next. Each rectangle has its name as a bold amber monospace heading.

Stage 1: DEV. Stage 2: CI. Stage 3: REGISTRY. Stage 4: IAC. Stage 5: CLUSTER. Stage 6: OPS.

Below each stage rectangle, stack a vertical column of small chips labeled with the controls that apply at that stage. Each chip has a tiny magenta security-shield icon to its left.

Under DEV: pre-commit hooks (lint, format), Conventional Commits (in editor), secret scanner (pre-push).

Under CI: pr-validation-template (Conventional Commits), tests + lint, build-push-generic with TRIVY scan, SBOM generation, (planned) Cosign sign.

Under REGISTRY: image signature verification, retention policy (cleanup-dockerhub), private by default.

Under IAC: Sealed Secrets (encrypted in git), Helm versions pinned, External Secrets (read from KMS), CODEOWNERS gates on merge.

Under CLUSTER: Pod Security Admission (restricted), NetworkPolicy default-deny, RBAC by least privilege, validation Jobs post-deploy.

Under OPS: Velero scheduled backups, audit log forwarding, Prometheus alerting, webhook-notification on failure.

The chips that correspond to templates or components shipped by AItizate/gh-actions-templates (pr-validation-template, build-push-generic with TRIVY, webhook-notification, plus Sealed Secrets and validation Jobs from the Forjate components catalog) have a stronger magenta border to highlight them as already-shipped controls vs nice-to-have advice.

Below the 6-stage strip, a horizontal dim-cyan callout band reading: every gate is opt-in. compose your security posture from the catalog. magenta-bordered chips are already shipped today.

At the very bottom of the image, a single horizontal amber bar in monospace reading DEVSECOPS — SECURITY AS CODE. SHIPPED WITH THE PLATFORM.

A tiny terminal artifact in the bottom-left corner reads > aitizate:devsecops-gates_v0.1 in cyan monospace. Generous whitespace despite six-stage density. Polished but with a hint of late-night sysadmin gloom."'
```

## Iteration log

| Version | Notes |
|---------|-------|
| **v0.1** | **Final.** Approved on first pass. Single quirk: stage headings rendered in cyan instead of amber as instructed — accepted as cosmetic. |
