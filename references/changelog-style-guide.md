# Mixpanel Changelog Style Guide

Derived from the docs repo (github.com/mixpanel/docs/pages/changelogs) and the internal [How and when to add a new product update to the changelog](https://www.notion.so/mxpnl/How-and-when-to-add-a-new-product-update-to-the-changelog-130e0ba9256280a98087f8dbafe0fa4c) guide. Update when patterns change.

---

## When to post a changelog

Post a changelog for **any change that materially affects the customer experience**. Small improvements in load time, moving a button, etc. don't get a dedicated changelog. If you're ever unsure, check with PMM.

Changelogs should go out **within one day of a change being GA** so customers have something to reference. This avoids cases where a customer asks about a new feature but there's no documentation of its release.

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
- `description`: Used as the preview text in the changelog feed. Keep under 200 characters. Go a layer deeper than the title — what does it do in detail, and why would someone use it?
- `isAnnouncement`: Set `true` for Tier 1 launches or critical updates. Announcement posts should have a custom hero image from the brand team. Most entries are `false`.
- `video`: Optional. If a demo video exists, include the Loom embed URL (e.g., `"https://www.loom.com/embed/..."`). Include both thumbnail and video when available so both appear in the feed.

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

## VideoButtonWithModal component

Use this component to embed demo videos with consistent formatting:

```mdx
<VideoButtonWithModal src="https://www.loom.com/embed/164cee809f034b6cb8db3e67adfd3d71" />
```

Place it at the end of the changelog body. The `video` field in frontmatter and this component serve different purposes — the frontmatter `video` field drives the feed preview, while this component renders the video inline on the changelog page.

---

## Title formats

Use **sentence case** (capitalize only the first word and proper nouns). No periods. Always use **colons** (not dashes or em dashes) to separate the product name from the benefit.

Always note beta status in the title if applicable (e.g., "now in beta").

### Title patterns by type of change

**Net-new feature** — lead with the outcome or feature name:
```
"[Big Outcome or Capability] with [Feature Name]"
"[Feature name] for [outcome]"
```
Examples:
- `"Connect your LLM metrics to Mixpanel with Langfuse integration"`

**Update to an existing product** — lead with the product name:
```
"[Product name]: [Outcome with] [name of change]"
```
Examples:
- `"Session Replay: Understand instantly with AI summaries"`

**Technical / backend / pricing / smaller fix** — keep it clear and straightforward:
```
"SSO, Data Views, and Sensitive Data Classification now available on Growth Plans"
```

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

## Learn More section

For medium and long changelog entries, structure the body as a "Learn More" section:

1. Open with what the feature does
2. Bullet the key value props (use **bold labels**)
3. End with a CTA linking to the docs
4. **Always include pricing/packaging details** — if it's only available on Enterprise, add a note. If it's an add-on, say so.

```mdx
Use dynamic config to update your application in real-time and target users
with different experiences, without changing code, all from one JSON payload.

With dynamic config, you can:
- **Go beyond on/off:** Control UI, logic, and defaults with structured parameters
- **Iterate faster:** Update configuration instantly without redeploys
- **Deliver tailored experiences:** Serve different configurations to different users

Build more adaptable product experiences with dynamic config. [Learn More →](/docs/featureflags#types-of-feature-flags)

**Note:** Dynamic config is available as part of the Feature Flagging add-on for enterprise customers.
```

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

### Image requirements

- Target size: **828x465** pixels
- For visual features, use a high-quality screenshot most representative of what it does, and include the feature name
- For non-visual features (backend, pricing, etc.), use text or an icon — or skip the image entirely
- Always use a **designed background** — no floating screenshots
- Announcement posts (`isAnnouncement: true`) should have a custom hero image from the brand/design team

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
