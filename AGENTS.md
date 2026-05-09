# AGENTS.md

Operational schema for maintaining this repository as an LLM-powered persistent knowledge wiki.

This file defines how AI agents should read, write, organize, update, and verify the wiki. The goal is to make the repo a compounding knowledge system instead of a loose collection of notes.

## Core mission

Agents maintain a persistent markdown wiki that compiles knowledge from raw sources, user conversations, research, experiments, and operational workflows.

The wiki should:

- Preserve source material separately from generated synthesis.
- Turn raw information into structured, interlinked markdown pages.
- Update existing pages when new information changes or refines prior understanding.
- Track contradictions, uncertainty, and stale claims.
- Keep an index and log current.
- Produce reusable outputs that can be filed back into the wiki.

## Repository structure

Use this structure by default:

```text
/
├── AGENTS.md
├── README.md
├── index.md
├── log.md
├── raw/
│   ├── sources/
│   └── assets/
├── wiki/
│   ├── concepts/
│   ├── entities/
│   ├── protocols/
│   ├── products/
│   ├── strategies/
│   ├── workflows/
│   └── synthesis/
├── agents/
│   ├── profiles/
│   ├── roles/
│   └── runs/
├── prompts/
│   ├── reusable/
│   ├── research/
│   ├── coding/
│   └── marketing/
├── research/
│   ├── notes/
│   ├── comparisons/
│   └── reports/
└── tools/
    ├── scripts/
    └── templates/
```

If a folder does not exist yet, create it when needed.

## Source of truth hierarchy

Agents must distinguish between source layers:

1. **Raw sources**: original documents, transcripts, screenshots, articles, code, CSVs, exports, and other primary materials. These should be preserved in `raw/sources/` or referenced clearly.
2. **Wiki pages**: LLM-generated summaries, entity pages, concept pages, comparisons, and synthesis files.
3. **Operational files**: `AGENTS.md`, `index.md`, `log.md`, templates, prompts, and workflow docs.
4. **Chat outputs**: useful answers, analyses, or plans from conversations that should be turned into durable wiki pages.

Raw sources should not be silently overwritten. Generated wiki pages may be updated as understanding improves.

## File naming conventions

Use lowercase kebab-case for file names.

Examples:

```text
wiki/concepts/concentrated-liquidity.md
wiki/protocols/aibtc.md
wiki/products/hodlmm.md
wiki/strategies/market-making-swarm.md
agents/profiles/liquidity-manager-agent.md
research/reports/sbtc-yield-vaults.md
```

Prefer stable names over clever names. One major concept, entity, product, protocol, or workflow per page.

## Page format

Most wiki pages should use this structure:

```markdown
---
title: Page Title
type: concept | entity | product | protocol | workflow | strategy | source-summary | synthesis
status: draft | active | needs-review | stale
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: []
sources: []
---

# Page Title

## Summary

Short explanation of what this page covers.

## Key points

- Important point 1.
- Important point 2.

## Details

Expanded explanation.

## Related pages

- [[related-page]]

## Open questions

- Question or uncertainty to investigate.

## Source notes

- Source-specific notes, links, or references.
```

Use YAML frontmatter when helpful. Keep it simple and consistent.

## Link conventions

Use Obsidian-style internal links when referencing other wiki pages:

```markdown
[[hodlmm]]
[[market-making-swarm]]
[[sbtc]]
```

If a referenced concept does not have a page yet, create a stub page or add it to `index.md` as a missing page candidate.

## Required operating files

### index.md

`index.md` is the content map of the wiki.

It should include:

- Major folders and page categories.
- Every important page with a one-line description.
- Missing/stub pages that should be created.
- High-value entry points for future agents.

Update `index.md` whenever creating, renaming, or materially changing wiki pages.

### log.md

`log.md` is the chronological operating record.

Every meaningful operation should append an entry using this format:

```markdown
## [YYYY-MM-DD] operation-type | Short Title

- Files created:
- Files updated:
- Sources used:
- Summary:
- Open follow-ups:
```

Operation types:

- `ingest`
- `query`
- `lint`
- `research`
- `synthesis`
- `agent-run`
- `maintenance`

## Workflows

### 1. Ingest workflow

Use this when a new source is added.

Steps:

1. Read the source carefully.
2. Identify the source type, author, date, scope, and reliability.
3. Create a source-summary page when useful.
4. Extract entities, concepts, workflows, claims, metrics, and contradictions.
5. Update existing relevant pages.
6. Create new pages for important concepts or entities.
7. Add internal links between related pages.
8. Update `index.md`.
9. Append an `ingest` entry to `log.md`.
10. List unresolved questions.

Do not just summarize. Integrate.

### 2. Query workflow

Use this when answering a question from the wiki.

Steps:

1. Read `index.md` first.
2. Identify the most relevant pages.
3. Read those pages before answering.
4. Synthesize an answer with clear uncertainty boundaries.
5. If the answer creates durable value, file it as a new page under `wiki/synthesis/`, `research/reports/`, or another suitable folder.
6. Update `index.md` and `log.md` if a durable page is created.

### 3. Lint workflow

Use this periodically to keep the wiki healthy.

Check for:

- Contradictions between pages.
- Stale claims.
- Orphan pages with no inbound links.
- Important repeated concepts without dedicated pages.
- Missing citations or weak source trails.
- Pages that should be merged or split.
- Folder drift or inconsistent naming.
- Open questions that have been answered elsewhere.

Output a concise lint report and create/update pages as needed.

### 4. Research workflow

Use this for active investigation.

Steps:

1. Define the research question.
2. Identify what is already known in the wiki.
3. Gather source material.
4. Separate facts from interpretation.
5. Create notes under `research/notes/`.
6. Create structured outputs under `research/reports/` or `wiki/synthesis/`.
7. Update related wiki pages.
8. Add open questions and next research targets.

### 5. Agent-run workflow

Use this for multi-agent or swarm experiments.

Each run should create a file under:

```text
agents/runs/YYYY-MM-DD-run-name.md
```

Run file template:

```markdown
---
title: Run Name
type: agent-run
status: planned | running | completed | failed
created: YYYY-MM-DD
updated: YYYY-MM-DD
agents: []
wallets: []
related_pages: []
---

# Run Name

## Objective

## Agents involved

## Inputs

## Actions taken

## Results

## Risks / issues

## Follow-ups
```

## Agent roles

Agents may specialize by role. Common roles:

### Wiki Maintainer

Responsible for structure, naming, cross-links, index updates, and log updates.

### Source Ingestor

Responsible for processing new documents and turning raw sources into integrated wiki knowledge.

### Research Analyst

Responsible for deep analysis, comparisons, market/protocol research, and synthesis reports.

### Protocol Analyst

Responsible for technical analysis of protocols, smart contracts, mechanisms, risks, and integrations.

### Liquidity Strategy Agent

Responsible for liquidity management notes, LP strategies, position logic, HODLMM research, and market-making workflows.

### Swarm Coordinator

Responsible for agent identities, role boundaries, schedules, wallet separation, run logs, and conflict avoidance.

### Marketing/Comms Agent

Responsible for turning wiki knowledge into copy, announcements, threads, guides, scripts, and campaign materials.

## Swarm-specific conventions

For AIBTC, HODLMM, liquidity, or market-making swarm research:

- Treat each agent as a distinct operational identity.
- Track each agent profile separately under `agents/profiles/`.
- Track wallet assumptions and permissions explicitly.
- Never mix live funds, test funds, and simulated funds in the same page without labeling them clearly.
- Record strategy assumptions before results.
- Record known risks, failure modes, and guardrails.
- Separate scheduling logic from trading/liquidity logic.
- Document cron jobs, triggers, and overlapping responsibilities.
- Treat any financial strategy as research unless explicitly marked as live operations.

## Citations and evidence

Agents should preserve source trails.

When using an external source, include:

- Source title.
- URL or local file path.
- Author or publisher when known.
- Date published or accessed when known.
- Notes on reliability or limitations.

When updating a claim because of new evidence, note what changed and why.

Avoid unsupported certainty. Use labels such as:

- Confirmed
- Likely
- Hypothesis
- Needs verification
- Deprecated
- Contradicted

## Handling contradictions

When new information conflicts with existing pages:

1. Do not erase the older claim silently.
2. Add a contradiction note.
3. Identify the stronger source if possible.
4. Update the page summary to reflect the current best understanding.
5. Add the issue to open questions if unresolved.

Suggested format:

```markdown
> Contradiction note: Source A says X, while Source B says Y. Current best interpretation: Z. Needs verification.
```

## Quality bar

Every durable page should be:

- Clear enough for a future agent to use without prior chat context.
- Linked to related pages.
- Dated or versioned when time-sensitive.
- Explicit about uncertainty.
- Free of unnecessary fluff.
- Useful as part of a larger knowledge system.

## Do not do

Agents must not:

- Dump raw summaries without integrating them.
- Delete source material without explicit instruction.
- Invent sources or citations.
- Collapse distinct concepts into one vague page.
- Leave major generated pages unlinked from `index.md`.
- Make financial, legal, medical, or security claims without uncertainty and source context.
- Treat chat history as durable memory unless it has been filed into the wiki.

## First setup tasks

After this file exists, initialize the wiki with:

1. `index.md`
2. `log.md`
3. `wiki/concepts/llm-wiki.md`
4. `wiki/workflows/ingest-workflow.md`
5. `wiki/workflows/query-workflow.md`
6. `wiki/workflows/lint-workflow.md`
7. `agents/roles/wiki-maintainer.md`
8. `agents/roles/swarm-coordinator.md`

## Default agent instruction

When operating in this repository, behave like a disciplined wiki maintainer and research operator.

Before writing, understand the current structure. After writing, update the map and log. Prefer durable, linked knowledge over disposable chat output.
