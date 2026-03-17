# Mixpanel Docs Style Guide

Derived from reading the actual docs repo (github.com/mixpanel/docs). Update this file when patterns in the live docs change.

---

## Page Types

The docs have two structural patterns:

**Index pages** — used for sections that have sub-pages (e.g., `data-structure.mdx`, `features.mdx`). These pages are almost entirely `<Cards>` components that link to child pages. Don't add prose to index pages.

```mdx
import { Cards } from 'nextra/components'

# Section Name

Optional one-line description.

<Cards>
  <Cards.Card icon title="Sub-page Name" href="/docs/section/sub-page" />
  ...
</Cards>
```

**Leaf pages** — actual content pages. Everything below applies to these.

---

## Page Title (H1)

Two formats are used. Choose based on context:

**Simple noun phrase** — use for foundational or reference content:
```
# Data Structure
# Reports Overview
# Tracking Best Practices
```

**Feature name + benefit** — use for product feature pages:
```
# Session Replay: Watch playbacks of user digital experiences
# Alerts: Get notified about anomalies in your data
```

Never use the colon format for index pages.

---

## Headings (H2 and below)

Use **Title Case** throughout — capitalize every significant word.

```
## Plan Availability       ✓
## Create an Alert         ✓
## View & Manage Alerts    ✓
### Custom Threshold       ✓
### Anomaly Detection      ✓

## plan availability       ✗
## Create an alert         ✗
```

Use `&` not "and" in headings when the heading would otherwise be long (e.g., `## View & Manage Alerts`).

---

## Opening Line

The first paragraph sets context. Write one or two direct sentences that describe what the feature does — no throat-clearing, no "Welcome to" framing, no preamble.

```
✓  "Mixpanel provides the ability to create alerts for your Insights and Funnels reports,
    allowing you to monitor custom report conditions or automatically detect anomalies."

✓  "Mixpanel Session Replay provides the fastest way to gain a comprehensive understanding
    of your customers by combining both quantitative and qualitative insights."

✗  "This article covers how to use alerts in Mixpanel."
✗  "In this guide, you'll learn about..."
```

---

## Plan Availability

If a feature is plan-gated, always put this **at the very top** of the page — before any other content — as a `<Callout type="info">` or a dedicated `## Plan Availability` section with a table.

**Simple gating** → use a Callout:
```mdx
<Callout type="info">
    Users with a paid plan can access Alerts. Growth plan users can set up to 5 alerts
    per project. Enterprise plan users can set an unlimited number of alerts. See our
    [pricing page](https://mixpanel.com/pricing/) for more details.
</Callout>
```

**Complex gating with multiple tiers** → use a table under `## Plan Availability`:
```mdx
## Plan Availability

| Plan       | Allowance              | How to Access |
|------------|------------------------|---------------|
| Free       | 10k free per month     | ...           |
| Growth     | 20k free per month     | ...           |
| Enterprise | 20k free per month     | Contact AM    |
```

---

## Numbered Steps

Bold the key action at the start of each step. Use `*Note: ...*` in italics for sub-notes within a step (not a Callout).

```mdx
1. **Save your report**, click the 3 dots icon, go to Alerts, and select Create Alert.
   *Note: You won't be able to create alerts if the report has unsaved changes.*

2. **Enter a name** for your alert.

3. **Set your alert criteria.**
```

---

## Callouts

Use `<Callout>` from nextra/components sparingly — for things the reader genuinely needs to know before proceeding, or important limitations.

```mdx
import { Callout } from 'nextra/components'

<Callout type="info">
    Content here. Can span multiple sentences.
</Callout>
```

- `type="info"` — most common; used for notes, plan restrictions, tips, beta notices
- `type="warning"` — use only for data loss risks or irreversible actions

Do not use Callouts for general information that could just be prose.

---

## Images

Two conventions exist in the codebase — both are fine:

```mdx
![](/filename.png)                                          # from /public, no alt text
![replayHeroImage](/replayHeroImageWithPrivacy.png)         # from /public, with alt text
![image](https://github.com/mixpanel/docs/assets/...)      # GitHub-hosted asset
```

**When to use each**:
- New screenshots → upload to `/public/` and reference as `/filename.png`
- Screenshots already uploaded to GitHub → use the GitHub asset URL

Place images **immediately after** the sentence or step that describes what the reader is looking at. Don't cluster images at the end of a section.

Image filenames in `/public/` use camelCase (e.g., `replayHeroImageWithPrivacy.png`, `webhookalert2.png`).

---

## FAQ Section

Use `####` (H4) for each question. Don't use bold or a different format.

```mdx
## FAQ

#### What happens when I reach my limit?

Answer text here.

#### How soon are replays available?

Answer text here.
```

---

## Changelog Entries

Changelogs live at `pages/changelogs/YYYY-MM-DD-slug.md`. Use this frontmatter exactly:

```md
---
title: "Short description of what changed"
slug: "changelog-YYYY-MM-DD-descriptive-slug"
hidden: false
createdAt: "YYYY-MM-DDT00:00:00.000Z"
updatedAt: "YYYY-MM-DDT00:00:00.000Z"
date: "YYYY-MM-DD"
---

One to three sentences. Describe what changed and why it's useful to users.

[Read more here.](https://docs.mixpanel.com/docs/...)
```

Titles are in quotes, title case. Keep the body short — 1–3 sentences max plus a link.

---

## Tone

- **Second person throughout** — "you", "your project", "your reports"
- **Present tense** for describing current product behavior
- **Active voice** — "Mixpanel calculates thresholds" not "thresholds are calculated by Mixpanel"
- **No marketing language** — don't describe features as "powerful", "robust", or "seamless" in prose (the docs use these words occasionally in feature descriptions, but avoid them in instructional content)
- **Functional** — tell the reader what to do or what they can expect; don't editorialize

---

## Components Reference

```mdx
import { Callout } from 'nextra/components'         # notes, warnings, plan info
import { Cards } from 'nextra/components'           # index page card grids
import ExtendedButton from "/components/ExtendedButton/ExtendedButton"  # CTA buttons (rare)
```

Raw HTML (`<br></br>`, `<div>`, `<iframe>`) is used sparingly on intro/marketing-style pages. Avoid it in standard feature docs.

---

## Internal Links

Use relative paths:
```mdx
[Cohorts](/docs/users/cohorts)
[Roles and Permissions](/docs/orgs-and-projects/roles-and-permissions)
[pricing page](https://mixpanel.com/pricing/)      # external links are absolute
```

---

## What to Avoid

- Sentence-case headings
- Starting with "This article covers..." or "In this guide..."
- `<Callout>` for things that could just be a sentence
- Grouping all images at the end of a section
- Long paragraphs — break up anything over ~5 sentences
- Describing limitations after the fact — surface them early (plan gating at top, known limitations in a dedicated section)
