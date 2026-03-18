# Mixpanel Docs Style Guide

Derived from the actual docs repo (github.com/mixpanel/docs) and the internal [Maintaining Docs: Internal Workflows](https://www.notion.so/mxpnl/Maintaining-Docs-Internal-Workflows-896613cc41324df48f2a6afd1dba7ac0) guide. For anything not covered here, fall back to the [Google Dev Docs Style Guide](https://developers.google.com/style).

---

## Audience

The docs serve two primary personas. Keep both in mind when writing:

| | Developers | Analysts |
|---|---|---|
| Typical roles | Engineers | PMs, Analysts, Marketers, Designers |
| Focus | Connecting data to Mixpanel | Creating and analyzing reports |
| Communication | Use basic terms when possible; industry-standard technical terms are fine when needed. Don't teach people how to code — be cursory on steps most engineers already understand. | Spell out terminology that is technical or specific to product analytics. Define a term the first time it appears. Err on the side of over-explaining each step. |

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

See `changelog-style-guide.md` in this directory for the full changelog format. Changelogs have a distinct tone from docs and warrant their own guide.

Short summary: files are `.mdx` (not `.md`), frontmatter includes `thumbnail`/`description`/`isAnnouncement`, body starts with `<ChangelogPostHeader />`, uses "we"/"our" company voice, and images go in `/public/changelog/` (not `/public/`).

---

## Tone

Our voice: **speak as a translator**. We're builders who use Mixpanel every day. Be plainspoken. Make the complex simple.

- **Second person throughout** — "you", "your project", "your reports"
- **Present tense** for describing current product behavior
- **Active voice** — "Mixpanel calculates thresholds" not "thresholds are calculated by Mixpanel"
- **No marketing language** — don't describe features as "powerful", "robust", or "seamless" in prose (the docs use these words occasionally in feature descriptions, but avoid them in instructional content)
- **Let the product speak for itself** — avoid claims like "we are fast." Let customers say that for us.
- **Functional** — tell the reader what to do or what they can expect; don't editorialize
- **Conversational, not corporate** — but keep it professional
- **Aim for timelessness** — avoid words like "now", "new", "update", "currently". These go stale fast.
- **Brevity is beautiful** — provide steps, not word salad. "Easy reading is damn hard writing."
- **Consistency** — once you use a term, keep using the same term throughout. Don't alternate between synonyms.
- **Read it out loud** — cut anything that makes you pause or question the meaning

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

## Punctuation & Grammar

- No exclamation points
- Oxford comma (like this, this, and this)
- Em dashes — put a space before and after
- Use "you" in almost all cases
- Use `%`, not "percent" — 100% of the time
- Title Case for product feature names inline (e.g., Insights Reports, Session Replay)

---

## Emphasis & Formatting

- Use **bold** for emphasis
- Do not use italics or underlines for emphasis
- Do not use emojis
- If a page has more than 2–3 H2 sections, consider breaking it into multiple pages

---

## Linking

- Keep hyperlinks within the relevant sentence
- A single link in a sentence should sit on the core keyword, not on "click here" or "learn more"
- If linking to 2–3 things, use the (here, here, and here) framing

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

### Screenshot guidelines

- **Focus on the relevant part** — you don't always need a full product view. Cropping to the key area creates focus.
- **Don't show navigation or browser bars** unless they're relevant to the concept being demonstrated. Leaving them out also prevents images from going stale as quickly.
- **Use demo data only** — never show customer data or internal Mixpanel data. Take special care that API credentials are not visible.
- **Use light mode** — the light color scheme works best on the white docs background. Dark mode is visually heavy and doesn't balance well.
- **Cross-reference copy and imagery** — if you add or update an image, double-check that surrounding text still matches.

### Alt text

- Brief — ideally under 125 characters
- Describe what the image shows and why it matters in context
- Don't start with "Image of" or "Picture of"
- Don't keyword-stuff — a few coherent phrases focused on description

---

## Video

Loom videos are acceptable in docs. Include them contextually with the relevant topic, not on standalone pages.

---

## Previewing Changes

When you create a PR against the docs repo, Vercel generates a preview at:
```
https://docs-git-<branch_name>-mixpanel.vercel.app/docs/what-is-mixpanel
```
Replace `<branch_name>` with your branch name.

---

## Redirects

The `redirects/` folder in the docs repo contains three files for managing URL redirects:

| File | Redirects |
|---|---|
| `local.txt` | docs → docs |
| `help-mixpanel-com.txt` | help → docs |
| `developer-mixpanel-com.txt` | developer → docs |

Format: `[incoming url] [destination]` — one per line.

---

## What to Avoid

- Sentence-case headings
- Starting with "This article covers..." or "In this guide..."
- `<Callout>` for things that could just be a sentence
- Grouping all images at the end of a section
- Long paragraphs — break up anything over ~5 sentences
- Describing limitations after the fact — surface them early (plan gating at top, known limitations in a dedicated section)
- Jargon or overly complex terminology — define technical terms for beginners
- $100 words — we don't "deduce complexities to surface invisible tensions." We "help teams see clearly."
