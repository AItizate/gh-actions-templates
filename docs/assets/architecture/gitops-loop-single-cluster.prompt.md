# GitOps Loop — Single Cluster

**Output:** `gitops-loop-single-cluster.png` (alongside this file)
**Aspect:** 16:9
**Approved version:** v0.1

The simplest possible GitOps loop: one app repo, one IAC repo, one ArgoCD, one Kubernetes cluster. Use this image to teach the concept of GitOps. For the production-grade multi-environment / multi-tenant version, see [`gitops-loop-multi-cluster.prompt.md`](./gitops-loop-multi-cluster.prompt.md).

## Command (v0.1 — final)

```bash
gemini -y -p '/generate "GitOps loop diagram showing how a new container image lands in a Kubernetes cluster after CI pushes it to the registry. Single 16:9 wide cinematic frame. Cyberpunk dystopian terminal aesthetic — dark deep-navy background #0A1428 with very subtle horizontal scanlines and faint grain noise. Cyan #5BB4FF primary accents, occasional magenta #FF5BBF and warm amber #FFB45B highlights on key labels. Monospace terminal-style font for chip labels, slightly bolder geometric sans for section titles. Slightly imperfect borders with subtle 1-2px chromatic drift on a few boxes. NO PHOTOS NO 3D NO LOGOS NO COMPANY NAMES NO WATERMARK.

CRITICAL: do NOT render any of these words anywhere in the image: LEFT, RIGHT, CENTER, COLUMN, SECTION, ROW, LAYOUT, AREA, UPPER, LOWER, TOP, BOTTOM, GROUP, PANEL, STAGE. Only render actual content labels.

LAYOUT (instructions for you only, do not write these on the image):

The image is structured as a circular GitOps loop with five elements positioned around the loop. Arrows connect them in a single direction (clockwise), conveying the cycle is continuous.

Top-left element — a rounded rectangle labeled APP REPO CI in cyan. Inside: chip Build + Scan + Push (from build-push-generic-template). Subtitle in tiny dim cyan monospace: pushed image tag = git SHA.

A thick cyan arrow flows rightward from APP REPO CI to the top-right element.

Top-right element — a rounded rectangle labeled CONTAINER REGISTRY in cyan. Inside: chip ghcr.io / Docker Hub / ECR. The image just pushed sits here with its SHA tag.

A thick cyan arrow flows downward from CONTAINER REGISTRY to the right-side element.

Right-side element (middle of the right edge) — a rounded rectangle labeled IAC REPO in amber (highlighted, the source of truth). Inside: chip kustomization.yaml (images: section) + chip Auto-update workflow (sync-app-image.yml). Subtitle in tiny dim cyan monospace: image tag bumped via PR or direct commit. Magenta annotation: SINGLE SOURCE OF TRUTH.

A thick cyan arrow flows leftward (toward the bottom-center) from IAC REPO labeled pulled by ArgoCD every 3 min.

Bottom-center element — a rounded rectangle labeled ARGOCD in cyan. Inside: chip Reconcile loop.

A thick cyan arrow flows upward from ARGOCD into the left element.

Left element — a large rounded rectangle labeled KUBERNETES CLUSTER in amber at the top. Inside: chips Pods (new image SHA running), Service, Ingress.

From this cluster element, a thin dotted cyan arrow loops back upward to APP REPO CI to close the cycle visually, with the label developer iterates in tiny dim cyan monospace.

In the very center of the loop (the middle of the circular layout), a magenta callout chip labeled NO ONE WRITES TO THE CLUSTER DIRECTLY. ONLY ARGOCD RECONCILES. with subtitle in tiny dim cyan: audit trail = git log of the IAC repo.

OUTSIDE the loop at the bottom, a horizontal cyan callout band with text in cyan monospace: rollback = revert a commit in the IAC repo. ArgoCD picks it up automatically.

At the very bottom of the image, a single horizontal amber bar in monospace reading GITOPS LOOP — GIT IS THE SOURCE. ARGOCD IS THE HAND.

A tiny terminal artifact in the bottom-left corner reads > aitizate:gitops-loop_v0.1 in cyan monospace. Generous whitespace. Polished but with a hint of late-night sysadmin gloom."'
```

## Iteration log

| Version | Notes |
|---------|-------|
| **v0.1** | **Final.** Approved on first pass. Single-cluster shape, kept as the entry-point diagram for teaching the GitOps concept. The multi-cluster variant lives in `gitops-loop-multi-cluster.prompt.md`. |
