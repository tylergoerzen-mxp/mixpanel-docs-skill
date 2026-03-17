# Mixpanel Changelog Style Guide

Derived from reading recent changelogs in github.com/mixpanel/docs/pages/changelogs. Update when patterns change.

---

## How changelogs differ from docs

| | Docs | Changelogs |
|---|---|---|
| Voice | "you" / "your" only | "we" / "our" + "you" / "your" |
| Tone | Instructional, functional | Announcement-forward, slightly warmer |
| Opening | One factual sentence | Can have a narrative hook first |
| Marketing language | Avoid | Acceptable in moderation |
| Length | As long as needed | Scales with feature significance |
| Headers | Title Case H2/H3 | Only use headers for longer entries |

---

## File format

Files live at `pages/changelogs/YYYY-MM-DD-slug.mdx` — note the `.mdx` extension, not `.md`.

---

## Frontmatter

```mdx
---
title: "Title of the changelog entry"
slug: "changelog-YYYY-MM-DD-descriptive-slug"
hidden: false
createdAt: "YYYY-MM-DDT00:00:00.000Z"
updatedAt: "YYYY-MM-DDT00:00:00.000Z"
date: "YYYY-MM-DD"
thumbnail: "/changelog/image-name.png"
description: "One sentence used as a meta description and summary card text."
isAnnouncement: false
---
```

**Field notes:**
- `thumbnail`: Path to a hero image, or `""` if none. Images for changelogs live in `/public/changelog/` (not `/public/` root) and are referenced as `/changelog/filename.png`.
- `description`: Used as the preview text in the changelog feed. Keep it to one sentence, focused on user benefit.
- `isAnnouncement`: Set `true` only for major launches — flagship features, significant platform expansions. Most entries are `false`.
- `video`: Optional field. Include as `video: ""` if you need to add it later, or omit entirely.

---

## ChangelogPostHeader component

Every changelog body must start with this component immediately after the frontmatter:

```mdx
<ChangelogPostHeader
  date="YYYY-MM-DD"
  image="/changelog/image-name.png"
  title="Title of the changelog entry"
/>
```

If there's no image, use `image=""`. The `date` and `title` must match the frontmatter exactly.

---

## Title formats

Three patterns are used — pick based on what reads most naturally:

```
"Feature Name: What it does"                        # colon + benefit
"Feature Area — Sub-feature Name"                   # em dash for sub-features
"Plain statement about what changed"                # for smaller updates
```

Examples:
- `"Metric Trees: Build your first draft instantly with AI"`
- `"Feature Flags — Group Cohort Targeting"`
- `"Postgres Connectors now in Public Beta"`
- `"Custom Alerts via webhook"`

Title Case throughout. Titles in changelogs can be slightly more evocative than doc page titles.

---

## Tone and voice

Changelogs use **company voice** alongside user voice — "we" is appropriate here in a way it isn't in docs.

```
✓  "We've introduced AI-Powered Event Suggestions for Templates."
✓  "Setting up a new board just got a little easier."
✓  "We're pleased to announce the Postgres Connector, now available in Public Beta."
✗  "This article describes the new Postgres Connector feature."
```

Some marketing-adjacent language is acceptable — "simpler", "smoother", "faster" — but don't overdo it. The entry should still feel like it's informing, not selling.

---

## Length and structure

Scale length to the significance of the change:

### Short (2–4 sentences + link)
For incremental improvements, default behavior changes, or deprecations that affect a narrow audience.

```mdx
<ChangelogPostHeader ... />

New Enterprise accounts now have Data Volume Monitoring (DVM) enabled by default.
Enterprise projects automatically monitor event volume, detect sudden or significant
spikes, and notify admins so they can take corrective action quickly. No manual
setup is required during project creation.

You can enable or disable DVM at any time from Lexicon > Data Volume Monitoring.

Learn more about DVM and configuration options in our [documentation](/docs/data-governance/data-volume-monitoring).
```

### Medium (lede + bullet list + link)
For feature launches with a clear list of new capabilities.

```mdx
<ChangelogPostHeader ... />

[One hook sentence that frames the update.]

[One or two sentences describing what was added and why it helps.]

**What's new:**
- **Bold label:** Description of capability
- **Bold label:** Description of capability
- **Bold label:** Description of capability

[Learn more →](/docs/path)
```

### Long (multiple H2/H3 sections)
Only for significant launches — major new features, deprecations with wide impact, or changes requiring action from users.

Use H2 (`##`) and H3 (`###`) sections. Headers are Title Case, same as docs.

---

## Opening patterns

The first line after `<ChangelogPostHeader>` sets the tone. Two approaches work:

**Factual lead** — states the change directly:
```
Feature flag rollout groups can now target **group cohorts** — cohorts built on a
group key dimension such as Company, Organization, or any custom group entity.
```

**Narrative hook** — a short orienting sentence before the main content:
```
Setting up a new board just got a little easier.
```
Use the narrative hook sparingly — only when there's a clear before/after contrast worth calling out.

---

## Feature bullet lists

For listing capabilities, use this format:
```mdx
**What's new:**
- **Bold label:** Description without repeating the label
- **Bold label:** Description

or

- **Bold label:** Description
- **Bold label:** Description
- **Bold label:** Description
```

Avoid generic labels like "Feature 1" or "Improvement". Each label should name the specific capability.

---

## Closing links

Every changelog entry should end with a link to the full docs page. Common formats:

```mdx
[Learn more →](/docs/path/to/page)

[Learn more about X →](/docs/path/to/page)

More details on how to get started in our [docs](/docs/path/to/page).

Learn more and get started [here](/docs/path/to/page).
```

The arrow `→` is conventional for the prominent link format.

---

## Images

Images for changelogs live in `/public/changelog/` and are referenced as `/changelog/filename.png`.

This is different from regular doc images, which live in `/public/` and are referenced as `/filename.png`.

```mdx
# Changelog image
![description](/changelog/featureName.png)

# Regular doc image
![description](/featureName.png)
```

---

## Plan / availability callouts

Don't use `<Callout>` in changelogs. Use a plain `**Note:**` inline instead:

```mdx
**Note:** Metric Trees are available as an add-on for Enterprise customers.
```

---

## Beta / GA labeling

Call out beta status clearly in the title or opening line. Common patterns:
- `"now available in Public Beta"`
- `"now generally available"`
- `"currently in beta"`

If a feature has plan restrictions, state them near the top — either in the opening paragraph or as a `**Note:**` after the main content.

---

## What not to do

- Don't use `<Callout>` components — these belong in docs, not changelogs
- Don't write in passive voice: "Users can now..." not "It is now possible to..."
- Don't use changelog entries to document how to use a feature in detail — link to the docs page for that
- Don't write a changelog for a bug fix unless it had meaningful user-facing impact
- Don't use `hidden: true` unless the entry is genuinely draft/staging only
