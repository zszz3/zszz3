# zszz3 Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create and publish the public `zszz3/zszz3` profile repository with the approved README and an automatically generated light/dark contribution snake.

**Architecture:** `README.md` is a static GitHub profile document that depends only on readme-typing-svg, shields.io, and generated SVG files on an orphan `output` branch. A single scheduled GitHub Actions workflow generates the two snake SVGs and publishes them without modifying `main`.

**Tech Stack:** GitHub Flavored Markdown, shields.io, readme-typing-svg, GitHub Actions, `Platane/snk/svg-only@v3`, `crazy-max/ghaction-github-pages@v5`, git, GitHub CLI.

---

## File Map

- Create: `README.md` — exact public profile content and links.
- Create: `.github/workflows/snake.yml` — daily/manual snake generation and `output` branch publication.
- Existing: `docs/superpowers/specs/2026-07-17-zszz3-profile-readme-design.md` — approved source of truth.
- Existing: `docs/superpowers/plans/2026-07-17-zszz3-profile-readme.md` — this execution plan.

### Task 1: Add the approved profile README

**Files:**
- Create: `README.md`
- Reference: `docs/superpowers/specs/2026-07-17-zszz3-profile-readme-design.md`

- [ ] **Step 1: Verify the profile README does not exist yet**

Run:

```bash
test ! -e README.md
```

Expected: exit code 0.

- [ ] **Step 2: Create the exact README**

Create `README.md` with:

```markdown
<div align="center">

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&width=600&lines=Hi%2C+I'm+wojiecihuo+%F0%9F%91%8B" alt="Hi, I'm wojiecihuo" />

</div>

---

## About Me

- 🏫 **Southeast University**
- 🎯 **Focus:** Backend · AI Agents · 3D Gaussian Splatting
- 🏆 **Experience:** ACMer

---

## Interests

![Backend Engineering](https://img.shields.io/badge/Backend-Engineering-0969DA?style=for-the-badge)
![AI Agents](https://img.shields.io/badge/AI-Agents-412991?style=for-the-badge)
![LLM / AI Infra](https://img.shields.io/badge/LLM%20%2F%20AI-Infra-0F766E?style=for-the-badge)
![3D Gaussian Splatting](https://img.shields.io/badge/3D%20Gaussian-Splatting-8A2BE2?style=for-the-badge)

---

## Projects

**Author**

- [AgentRecall](https://github.com/zszz3/AgentRecall) — Search, manage, and migrate AI coding agent sessions.
- [multi-agent-chat](https://github.com/zszz3/multi-agent-chat) — A local-first workbench for agents and workflows.

**Contributor**

- [agentscope-java](https://github.com/agentscope-ai/agentscope-java) — Agent-oriented programming for building LLM applications.

---

## lmao

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/zszz3/zszz3/output/github-contribution-grid-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/zszz3/zszz3/output/github-contribution-grid-snake.svg" />
  <img alt="GitHub contribution grid snake animation" src="https://raw.githubusercontent.com/zszz3/zszz3/output/github-contribution-grid-snake.svg" />
</picture>
```

- [ ] **Step 3: Verify required content and forbidden claims**

Run:

```bash
rg -n "wojiecihuo|Southeast University|Backend · AI Agents · 3D Gaussian Splatting|Experience:\*\* ACMer|LLM%20%2F%20AI|AgentRecall|multi-agent-chat|agentscope-java|zszz3/zszz3/output" README.md
! rg -n "Student|Baidu|Intern|Former|MeloMei|img.shields.io/badge/(Go|Java|TypeScript|Electron|React|Node)" README.md
git diff --check
```

Expected: the first command prints every approved section; the second prints nothing; `git diff --check` prints nothing.

- [ ] **Step 4: Commit the README**

Run:

```bash
git add README.md
git commit -m "feat: add GitHub profile README"
```

Expected: one commit creating `README.md`.

### Task 2: Add contribution snake automation

**Files:**
- Create: `.github/workflows/snake.yml`

- [ ] **Step 1: Verify the workflow does not exist yet**

Run:

```bash
test ! -e .github/workflows/snake.yml
```

Expected: exit code 0.

- [ ] **Step 2: Create the exact workflow**

Create `.github/workflows/snake.yml` with:

```yaml
name: Generate contribution snake

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10

    steps:
      - name: Generate light and dark snake SVGs
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-contribution-grid-snake.svg
            dist/github-contribution-grid-snake-dark.svg?palette=github-dark

      - name: Publish SVGs to the output branch
        uses: crazy-max/ghaction-github-pages@v5
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- [ ] **Step 3: Validate syntax and workflow contract**

Run:

```bash
ruby -e 'require "yaml"; YAML.load_file(".github/workflows/snake.yml"); puts "YAML OK"'
rg -n "workflow_dispatch|contents: write|Platane/snk/svg-only@v3|github.repository_owner|github-contribution-grid-snake-dark.svg\?palette=github-dark|crazy-max/ghaction-github-pages@v5|target_branch: output|secrets.GITHUB_TOKEN" .github/workflows/snake.yml
git diff --check
```

Expected: `YAML OK`, every workflow contract line, and no whitespace errors.

- [ ] **Step 4: Commit the workflow**

Run:

```bash
git add .github/workflows/snake.yml
git commit -m "feat: generate contribution snake"
```

Expected: one commit creating the workflow.

### Task 3: Run complete local verification

**Files:**
- Verify: `README.md`
- Verify: `.github/workflows/snake.yml`
- Verify: `docs/superpowers/specs/2026-07-17-zszz3-profile-readme-design.md`

- [ ] **Step 1: Verify the expected repository shape**

Run:

```bash
rg --files --hidden -g '!.git' | sort
```

Expected files:

```text
.github/workflows/snake.yml
README.md
docs/superpowers/plans/2026-07-17-zszz3-profile-readme.md
docs/superpowers/specs/2026-07-17-zszz3-profile-readme-design.md
```

- [ ] **Step 2: Check every external URL**

Run:

```bash
curl -fsSIL https://github.com/zszz3/AgentRecall
curl -fsSIL https://github.com/zszz3/multi-agent-chat
curl -fsSIL https://github.com/agentscope-ai/agentscope-java
curl -fsSIL "https://readme-typing-svg.demolab.com?font=Fira+Code&size=22&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&width=600&lines=Hi%2C+I'm+wojiecihuo+%F0%9F%91%8B"
curl -fsSIL "https://img.shields.io/badge/LLM%20%2F%20AI-Infra-0F766E?style=for-the-badge"
```

Expected: every command exits 0 with an HTTP 2xx or redirect chain ending in 2xx.

- [ ] **Step 3: Verify commits and a clean worktree**

Run:

```bash
git log --oneline --decorate -4
git status --short
```

Expected: design, plan, README, and workflow commits are present; `git status --short` prints nothing.

### Task 4: Publish and verify the profile repository

**Files:**
- Publish all committed files to `https://github.com/zszz3/zszz3`

- [ ] **Step 1: Ensure GitHub CLI is authenticated as zszz3**

Run:

```bash
gh auth status
```

Expected: `Logged in to github.com account zszz3`. If the saved token is invalid, run `gh auth login -h github.com -w` and complete the browser authorization before continuing.

- [ ] **Step 2: Create and push the public profile repository**

Run:

```bash
gh repo create zszz3/zszz3 --public --source=. --remote=origin --push --description "GitHub profile README"
```

Expected: GitHub creates `zszz3/zszz3`, `origin` points to it, and `main` is pushed.

- [ ] **Step 3: Manually run the snake workflow**

Run:

```bash
gh workflow run snake.yml --repo zszz3/zszz3
gh run list --workflow snake.yml --repo zszz3/zszz3 --limit 1
```

Expected: one queued or in-progress run for `Generate contribution snake`.

- [ ] **Step 4: Watch the workflow and verify generated assets**

Run:

```bash
run_id=$(gh run list --workflow snake.yml --repo zszz3/zszz3 --limit 1 --json databaseId --jq '.[0].databaseId')
test -n "$run_id"
gh run watch "$run_id" --repo zszz3/zszz3 --exit-status
curl -fsSIL https://raw.githubusercontent.com/zszz3/zszz3/output/github-contribution-grid-snake.svg
curl -fsSIL https://raw.githubusercontent.com/zszz3/zszz3/output/github-contribution-grid-snake-dark.svg
```

Expected: the workflow exits successfully and both URLs return HTTP 200.

- [ ] **Step 5: Verify the public profile**

Run:

```bash
curl -fsSL https://github.com/zszz3 | rg -n "wojiecihuo|Southeast University|AgentRecall|agentscope-java"
```

Expected: the rendered public profile contains all four strings.
