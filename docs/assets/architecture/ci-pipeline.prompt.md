# CI Pipeline

**Output:** `ci-pipeline.png` (alongside this file)
**Aspect:** 16:9
**Approved version:** v0.2

End-to-end CI pipeline driven by `AItizate/gh-actions-templates`. Shows where each reusable template plugs in: PR validation, build + Trivy scan + push, release tagging, failure notification. Also includes a `COMING SOON — AGENTIC AUTOMATION` strip indicating where future AI agents will plug into the flow.

## Command (v0.2 — final)

```bash
gemini -y -p '/generate "End-to-end CI pipeline diagram for AItizate/gh-actions-templates. Shows the lifecycle of a developer commit through the reusable workflows, PLUS a coming-soon strip indicating where future AI agents will plug into the flow. Single 16:9 wide cinematic frame. Cyberpunk dystopian terminal aesthetic — dark deep-navy background #0A1428 with very subtle horizontal scanlines and faint grain noise. Cyan #5BB4FF primary accents, occasional magenta #FF5BBF and warm amber #FFB45B highlights on key labels. Monospace terminal-style font for chip labels, slightly bolder geometric sans for section titles. Slightly imperfect borders with subtle 1-2px chromatic drift on a few boxes. NO PHOTOS NO 3D NO LOGOS NO COMPANY NAMES NO WATERMARK.

CRITICAL: do NOT render any of these words anywhere in the image: LEFT, RIGHT, CENTER, COLUMN, SECTION, ROW, LAYOUT, AREA, UPPER, LOWER, TOP, BOTTOM, GROUP, PANEL, STAGE. Only render actual content labels.

LAYOUT (instructions for you only, do not write these on the image):

On the left side of the image, a rounded rectangle labeled DEVELOPER in cyan. Inside: a small user icon and a chip labeled COMMIT + PUSH. A single horizontal arrow flows rightward into a chip labeled PULL REQUEST that sits at the start of the central pipeline.

Across the middle of the image, a horizontal pipeline of 5 connected chips with thick cyan arrows between them, all sitting inside a wide rounded rectangle labeled GITHUB ACTIONS PIPELINE in amber at the top:

1. PULL REQUEST (entry chip, magenta-bordered)
2. pr-validation-template (Conventional Commits, sticky comment) — magenta-bordered, label below in tiny amber monospace: DevSecOps gate #1
3. tests + lint (consumer-supplied) — cyan-bordered
4. build-push-generic-template (build + TRIVY SCAN + push) — magenta-bordered, label below in tiny amber monospace: DevSecOps gate #2
5. push to registry — cyan-bordered

Below the build-push chip, a magenta vertical sub-callout that reads in monospace: TRIVY — fails on CRITICAL or HIGH. ignore-unfixed. blocks push.

Between chip 4 and chip 5, the arrow has a small magenta diamond on it labeled SCAN PASSED?. If it fails, a downward red-tinted arrow exits the pipeline toward the bottom and goes into a chip labeled webhook-notification-template, then to a chip labeled SLACK / DISCORD outside the pipeline.

After chip 5 (push to registry), the pipeline continues with TWO output paths:
- One thick cyan arrow goes rightward to a chip labeled CONTAINER REGISTRY (ghcr.io / Docker Hub / ECR).
- Another arrow conditionally branches downward toward a chip labeled release-tag-template, then to a chip labeled GITHUB RELEASE + GIT TAG.

OUTSIDE the pipeline on the right side, a chip labeled CONTAINER REGISTRY (ghcr.io / Docker Hub / ECR) receiving the registry-bound arrow.

OUTSIDE the pipeline at the bottom of the failure flow, a chip labeled webhook-notification-template magenta-bordered, with an arrow going further right to a small chip labeled SLACK / DISCORD / MATTERMOST.

Below the pipeline (and below the failure path), a horizontal cyan callout band with text in cyan monospace: every reusable template lives in AItizate/gh-actions-templates. consumers pin to @v1.

Below that cyan band, ADD a wider magenta-dashed-bordered strip labeled COMING SOON — AGENTIC AUTOMATION in magenta monospace heading. Inside this strip, four small ghost-style chips with thin dashed magenta borders, arranged horizontally with subtle spacing:
- AI PR REVIEW (deeper than Conventional Commits)
- AUTO-FIX CVES (rebuilds image after dependency bumps)
- CROSS-REPO ISSUE SYNC (open issues in downstream repos when this CI breaks them)
- TREND DETECTION (security regression and dependency drift over time)

From this COMING SOON strip, draw THIN DASHED MAGENTA LINES going UPWARD to the chips in the pipeline where each agent would plug in:
- AI PR REVIEW dashed-line to pr-validation-template (chip 2)
- AUTO-FIX CVES dashed-line to build-push-generic-template (chip 4)
- CROSS-REPO ISSUE SYNC dashed-line to webhook-notification-template
- TREND DETECTION dashed-line to push to registry (chip 5)

Each dashed line has a tiny label in dim magenta monospace: hooks into. The dashes are visibly different from the solid arrows of the main flow.

At the very bottom of the image, a single horizontal amber bar in monospace reading CI PIPELINE — VALIDATE. BUILD. SCAN. PUSH. TAG. NOTIFY.

A tiny terminal artifact in the bottom-left corner reads > aitizate:ci-pipeline_v0.2 in cyan monospace. Generous whitespace despite dense info. Polished but with a hint of late-night sysadmin gloom."'
```

## Iteration log

| Version | Notes |
|---------|-------|
| v0.1 | First pass — pipeline + DevSecOps gates + failure path + release branch. Approved structure but missing the agentic-automation roadmap. |
| **v0.2** | **Final.** Added COMING SOON — AGENTIC AUTOMATION strip below the cyan band, with four ghost-style chips (AI PR Review, Auto-fix CVEs, Cross-repo Issue Sync, Trend Detection) and dashed magenta lines tying them to the pipeline chips they would plug into. Model also added a decorative title/subtitle at the top (subtitle text is glitched but the visual works); accepted as cosmetic. |
