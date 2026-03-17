# mixpanel-docs skill

A Claude Code skill for writing and updating [Mixpanel's public documentation](https://docs.mixpanel.com). Point it at a PRD and a GitHub PR, and it handles the rest — finding the right place in the docs, asking the right questions, drafting MDX in Mixpanel's style, and opening a PR to the docs repo.

## What it does

1. **Asks for source materials** — PRD link and relevant GitHub PR(s)
2. **Researches in parallel** — reads the PRD, diffs the PRs, and browses the live [mixpanel/docs](https://github.com/mixpanel/docs) repo structure
3. **Proposes a location** in the docs nav and waits for confirmation
4. **Asks clarifying questions** — plan gating, beta status, behavior changes, cross-links
5. **Requests screenshots** as an explicit checklist, flagged as required from the writer
6. **Drafts the MDX doc** following Mixpanel's actual style (see `references/style-guide.md`)
7. **Drafts the changelog entry** alongside the doc
8. **Offers to open a draft PR** to `mixpanel/docs` with placeholder image notes — or hands you the MDX to copy in yourself

## Installation

### Claude Code (recommended)

Copy `mixpanel-docs.md` (the flattened command file) to your Claude Code commands directory:

```bash
cp mixpanel-docs.md ~/.claude/commands/mixpanel-docs.md
```

Then invoke it with `/mixpanel-docs` in any Claude Code session.

> The style guide is embedded in the command file. No other files needed for the command version.

### Full skill (with separate style guide reference)

If you want the skill in its structured form (e.g., for packaging with the Anthropic skill tools):

```
mixpanel-docs/
├── SKILL.md                      # Main skill instructions
└── references/
    └── style-guide.md            # Mixpanel docs style patterns
```

Point Claude at `SKILL.md` and it will load `references/style-guide.md` as needed.

## Style guide

`references/style-guide.md` is derived from reading the actual [mixpanel/docs](https://github.com/mixpanel/docs) repo. It covers:

- Page types (index vs. leaf pages)
- H1 and heading formatting (Title Case, colon patterns)
- Plan availability placement
- Numbered step formatting
- Callout usage (`type="info"` vs `type="warning"`)
- Image conventions and filenames
- Changelog frontmatter format
- Tone and voice rules

Update this file when the live docs diverge from these patterns.

## Requirements

- Claude Code with `gh` CLI authenticated to GitHub
- Access to `github.com/mixpanel/docs` (public repo — no auth needed to read, write access needed to open PRs)
