# GitOps Loop — Multi Cluster

**Output:** `gitops-loop-multi-cluster.png` (alongside this file)
**Aspect:** 16:9
**Approved version:** v0.2

The production-grade GitOps loop: one IAC repo with multiple overlays (dev / staging / prod, or per-tenant), one ArgoCD with ApplicationSet fanning out to N clusters. The same pattern serves multi-environment promotions and cluster-per-tenant isolation. The conceptual single-cluster intro lives in [`gitops-loop-single-cluster.prompt.md`](./gitops-loop-single-cluster.prompt.md).

## Command (v0.2 — final)

```bash
gemini -y -p '/generate "GitOps loop diagram showing how a new container image lands in MULTIPLE Kubernetes clusters after CI pushes it to the registry. A single IAC repo holds the manifests for every environment and tenant; a single ArgoCD instance reconciles N target clusters. Single 16:9 wide cinematic frame. Cyberpunk dystopian terminal aesthetic — dark deep-navy background #0A1428 with very subtle horizontal scanlines and faint grain noise. Cyan #5BB4FF primary accents, occasional magenta #FF5BBF and warm amber #FFB45B highlights on key labels. Monospace terminal-style font for chip labels, slightly bolder geometric sans for section titles. Slightly imperfect borders with subtle 1-2px chromatic drift on a few boxes. NO PHOTOS NO 3D NO LOGOS NO COMPANY NAMES NO WATERMARK.

CRITICAL: do NOT render any of these words anywhere in the image: LEFT, RIGHT, CENTER, COLUMN, SECTION, ROW, LAYOUT, AREA, UPPER, LOWER, TOP, BOTTOM, GROUP, PANEL, STAGE. Only render actual content labels.

LAYOUT (instructions for you only, do not write these on the image):

Top-left element — a rounded rectangle labeled APP REPO CI in cyan. Inside: chip Build + Scan + Push (from build-push-generic-template). Subtitle in tiny dim cyan monospace: pushed image tag = git SHA.

A thick cyan arrow flows rightward from APP REPO CI to:

Top-right element — a rounded rectangle labeled CONTAINER REGISTRY in cyan. Inside: chip ghcr.io / Docker Hub / ECR.

A thick cyan arrow flows downward from CONTAINER REGISTRY to:

Right-side element (middle of the right edge) — a rounded rectangle labeled IAC REPO in amber (highlighted, the source of truth). Inside, three small stacked chips representing overlays: dev/ overlay, staging/ overlay, prod/ overlay. Below them a smaller chip Auto-update workflow (sync-app-image.yml) bumps the right overlay based on the trigger. Subtitle in tiny dim cyan monospace: one repo. N overlays. Magenta annotation: SINGLE SOURCE OF TRUTH.

A thick cyan arrow flows leftward (toward the bottom-center) from IAC REPO labeled pulled by ArgoCD every 3 min.

Bottom-center element — a hexagonal magenta chip labeled ARGOCD with a smaller subtitle ApplicationSet. From this hexagon, THREE distinct cyan arrows fan out leftward and upward to the three clusters described below. Each arrow has a tiny label naming which overlay path is being applied.

Three Kubernetes clusters arranged in a vertical stack on the left half of the image, each as its own small rounded rectangle:
- CLUSTER DEV — amber heading, smaller. Inside: chips Pods (dev SHA), Service, Ingress. Annotation: reconciled from dev/ overlay.
- CLUSTER STAGING — amber heading. Inside: chips Pods (staging SHA), Service, Ingress. Annotation: reconciled from staging/ overlay.
- CLUSTER PROD — amber heading. Inside: chips Pods (prod SHA), Service, Ingress. Annotation: reconciled from prod/ overlay.

Each cluster receives ONE of the three fan-out arrows from ArgoCD, terminating at its top edge.

From the bottom cluster (CLUSTER PROD), a thin dotted cyan arrow loops back upward to APP REPO CI to close the cycle visually, with the label developer iterates in tiny dim cyan monospace.

Floating between the three clusters and the IAC repo, a small magenta callout chip labeled ONE IAC REPO. ONE ARGOCD. N CLUSTERS. with subtitle in tiny dim cyan: works the same for multi-tenant (cluster-per-tenant) and multi-env (dev / staging / prod).

OUTSIDE the loop at the very bottom, a horizontal cyan callout band with text in cyan monospace: rollback = revert a commit in the IAC repo. all affected clusters converge automatically.

At the very bottom of the image, a single horizontal amber bar in monospace reading GITOPS LOOP — GIT IS THE SOURCE. ARGOCD IS THE HAND. N CLUSTERS ARE THE BODY.

A tiny terminal artifact in the bottom-left corner reads > aitizate:gitops-loop_v0.2 in cyan monospace. Generous whitespace. Polished but with a hint of late-night sysadmin gloom."'
```

## Iteration log

| Version | Notes |
|---------|-------|
| v0.1 (kept separately) | Single-cluster version. Approved. Kept as the entry-point diagram in `gitops-loop-single-cluster.prompt.md` to teach the GitOps concept simply. |
| **v0.2** | **Final.** Production-grade multi-cluster shape. IAC repo holds three overlays (dev/staging/prod); ArgoCD ApplicationSet fans out to three clusters. Same pattern serves multi-tenant (one cluster per tenant) and multi-env (dev/staging/prod). |
