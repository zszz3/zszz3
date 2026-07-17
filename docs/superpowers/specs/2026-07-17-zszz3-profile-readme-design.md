# zszz3 GitHub Profile README Design

## Goal

Create the `zszz3/zszz3` profile repository and a compact English-first README inspired by the information hierarchy of `MeloMei/MeloMei`. The result should feel familiar without copying MeloMei's personal claims or presenting unconfirmed information about zszz3.

## Design Direction

Use the approved balanced layout:

1. animated centered greeting;
2. concise About Me facts;
3. interest badges without a language or framework inventory;
4. projects grouped by relationship;
5. an automatically updated contribution snake.

The page should remain readable in both GitHub light and dark themes and should not require custom CSS or JavaScript.

## Approved Profile Content

### Identity

- Display name: `wojiecihuo`
- Affiliation: `Southeast University`
- Focus: `Backend · AI Agents · 3D Gaussian Splatting`
- Experience: `ACMer`

Do not claim that the user is a student, name a major or year, show a city, mention an employer or internship, or use the word `Former`.

### Interests

Show only these four interest badges:

- Backend Engineering
- AI Agents
- LLM / AI Infra
- 3D Gaussian Splatting

Do not add language badges or framework/tool badges. In particular, omit Go, Java, TypeScript, Electron, React, Node.js, and MCP from the badge section.

### Projects

Group projects by the user's relationship to them.

**Author**

- [AgentRecall](https://github.com/zszz3/AgentRecall) — Search, manage, and migrate AI coding agent sessions.
- [multi-agent-chat](https://github.com/zszz3/multi-agent-chat) — A local-first workbench for agents and workflows.

**Contributor**

- [agentscope-java](https://github.com/agentscope-ai/agentscope-java) — Agent-oriented programming for building LLM applications.

Do not label `agentscope-java` as authored, maintained, or owned by zszz3.

## README Structure

### Header

Use `readme-typing-svg` in a centered HTML block. The single greeting is:

`Hi, I'm wojiecihuo 👋`

The image must have useful alt text so the greeting remains understandable if the third-party image service is unavailable.

### About Me

Use three compact bullets:

- `Southeast University`
- `Focus: Backend · AI Agents · 3D Gaussian Splatting`
- `Experience: ACMer`

### Interests

Render four `shields.io` badges in the approved order. Badge colors should distinguish the four topics while remaining legible in both themes.

### Projects

Use simple Markdown links and one-line descriptions under `Author` and `Contributor` subheadings. Do not embed time-sensitive star counts in prose.

### Contribution Snake

End with the playful `lmao` heading from the reference structure and render the user's own contribution snake. Use a `<picture>` element with separate light and dark SVG sources from the `output` branch of `zszz3/zszz3`.

## Automation

Add `.github/workflows/snake.yml` with:

- manual `workflow_dispatch`;
- a daily schedule;
- `contents: write` permission;
- generation for GitHub user `zszz3`;
- light and dark SVG outputs;
- publication to an orphan `output` branch.

Use current, documented action releases and pin action versions rather than following an unversioned branch.

The workflow should be safe to rerun and should replace generated assets without changing README content.

## Failure Behavior

- Third-party header and badge images must include meaningful alt text.
- If the snake workflow has not run yet, only the snake image is absent; the rest of the README remains intact.
- A failed scheduled workflow must not modify `main`.
- The workflow must use only the repository-scoped `GITHUB_TOKEN`; no personal token or secret is required.

## Verification

Before publishing:

1. inspect the README source for the exact approved facts and omissions;
2. validate workflow YAML syntax and required permissions;
3. check all repository and image URLs;
4. verify no placeholder text or MeloMei-owned asset remains;
5. review the Markdown structure in light and dark theme assumptions.

After publishing:

1. manually dispatch the snake workflow;
2. confirm the workflow succeeds and creates the `output` branch;
3. confirm both light and dark SVGs load from `zszz3/zszz3`;
4. open the public profile and confirm the README renders.

## Repository Scope

The initial repository contains:

- `README.md`
- `.github/workflows/snake.yml`
- this design specification
- the implementation plan produced after design approval

No unrelated profile widgets, contact links, GitHub statistics cards, visitor counters, or extra automation are included.
