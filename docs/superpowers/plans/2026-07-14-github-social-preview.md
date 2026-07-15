# GitHub Social Preview Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Generate, validate, integrate, and publish a 1280×640 social-preview banner for the Facebook Invites Skill repository.

**Architecture:** Generate one production-quality raster image from the approved design specification, save it under `assets/`, and reference it near the top of the README. Validate the image dimensions, repository diff, and sensitive-data constraints before committing and pushing to `main`.

**Tech Stack:** Built-in image generation, PNG, PowerShell, Git, GitHub CLI.

## Global Constraints

- Canvas must be 1280×640.
- Primary text must be exactly `Facebook Invites Skill`.
- Secondary text must be exactly `Load • Invite • Verify`.
- No Facebook or GitHub logo, copied interface, page names, sports branding, profile photos, usernames, reaction counts, credentials, watermark, or extra text.
- Final asset path must be `assets/facebook-invites-social-preview.png`.

---

### Task 1: Generate and validate the social-preview asset

**Files:**
- Create: `assets/facebook-invites-social-preview.png`
- Reference: `docs/superpowers/specs/2026-07-14-github-social-preview-design.md`

**Interfaces:**
- Consumes: the approved visual specification and exact copy.
- Produces: a 1280×640 PNG suitable for GitHub social previews and README display.

- [ ] **Step 1: Generate the banner**

Use the built-in image-generation capability with the approved dark-tech prompt, exact title and subtitle, right-side abstract workflow illustration, and all constraints from the design specification.

- [ ] **Step 2: Save the selected output**

Copy the generated file to:

```text
assets/facebook-invites-social-preview.png
```

- [ ] **Step 3: Validate the asset**

Run a PNG metadata check and confirm:

```text
Width: 1280
Height: 640
Format: PNG
```

Visually confirm the exact title, exact subtitle, readable thumbnail hierarchy, neutral abstract UI, and absence of prohibited branding or private data.

### Task 2: Integrate and publish the asset

**Files:**
- Modify: `README.md`
- Create: `assets/facebook-invites-social-preview.png`
- Create: `docs/superpowers/plans/2026-07-14-github-social-preview.md`

**Interfaces:**
- Consumes: the validated PNG from Task 1.
- Produces: a public README image reference and pushed Git commit.

- [ ] **Step 1: Add the README image**

Insert this line immediately after the H1 heading:

```markdown
![Facebook Invites Skill social preview](assets/facebook-invites-social-preview.png)
```

- [ ] **Step 2: Verify the repository**

Run:

```powershell
git diff --check
git status -sb
```

Expected: no whitespace errors and only the image, README, plan, and approved design-spec commit are in scope.

- [ ] **Step 3: Scan for sensitive data**

Search the changed text for page names, personal paths, API keys, access tokens, private-key markers, and common credential formats. Expected: no matches outside explanatory security language.

- [ ] **Step 4: Commit and push**

```powershell
git add -- README.md assets/facebook-invites-social-preview.png docs/superpowers/plans/2026-07-14-github-social-preview.md
git commit -m "Add repository social preview"
git push origin main
```

- [ ] **Step 5: Verify GitHub**

Confirm the public repository remains `PUBLIC`, `main` contains the new commit, and the image path is available remotely.
