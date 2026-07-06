# Clean Enough House - Master Workflow

## Blog Identity

**Name:** Clean Enough House
**Tagline:** One mom's battle for a clean house
**URL:** https://cleanenoughhouse.com
**Protagonist:** Emily — late-30s graphic designer, homeschool mom, believer, married 10 years to Lucas
**Voice Model:** Dana White (A Slob Comes Clean) calibrated for a steadier, late-30s narrator (see SUSVoice.md)

---

## What This Blog Is

A long-running blog about the actual work of holding a household together while doing other things — running a business, raising kids, supporting a marriage, being a person. It's not an organizing blog dressed up with personality. It's a personal blog where organizing is one of the things that happens because keeping a house is one of the things adults do.

The reader comes back for **the people** (Emily, Lucas, Joey, Gracie, the wider cast), **the voice** (honest, self-deprecating, not performative), and **the continuity** (a world she recognizes after a few visits, not a series of evergreen advice columns).

Methods exist. Frameworks exist. They get taught when teaching them serves a moment. They are not the engine.

---

## Schedule

**Publishing cadence:** Two posts per week.

| Day | Slot | Time |
|-----|------|------|
| Tuesday | **Anchor** post | 9:00 AM CT |
| Thursday | **Lighter** post | 9:00 AM CT |

**Timezone:** America/Chicago.
- Central Standard Time (Nov–Mar): `T09:00:00-06:00`
- Central Daylight Time (Mar–Nov): `T09:00:00-05:00`

**Never publish:** Saturdays or Sundays. If a Tuesday or Thursday is unworkable, push to the next slot, don't substitute a weekend.

---

## The Two Slots

### Anchor (Tuesday)

The substantial post of the week. Story plus teaching, or deep teaching, or a real zone reckoning. Affiliate links live here primarily.

- **Length:** 1,200–2,500 words depending on format
- **Formats available:** Disaster Chronicle, Method Tutorial, Zone Transformation, Product Roundup, Quick Win, Myth Buster, System Breakdown (see SUSPostTypes.md)
- **Affiliate posture:** Anchor posts carry 1–2 affiliate products by default — this is where the blog's affiliate revenue lives. Maximum 2 products per post, ever. The one exception: a post whose own argument works against recommending a purchase (e.g. a Myth Buster arguing a problem is structural, not solvable by buying something) may run dry on purpose. "Dry by design" is a deliberate editorial call, not the default — most Anchors should sell.
- **Origin:** Usually starts from "I want to teach this" or "this story is worth telling at length."

### Lighter (Thursday)

The variety slot. Shorter, more flexible, lower stakes. This is where the blog gets its texture and where readers feel like they know these people.

- **Length:** 600–900 words typically (a longer Lighter is fine if the moment calls for it)
- **Formats available:** Field Notes, Q&A, List with Personality, Status Report, The Observation, Letters, Photo Walk (see SUSPostTypes.md)
- **Affiliate posture:** Low to none. If a product comes up organically, fine. Don't force it.
- **Origin:** Usually starts from "something happened this week" or "I noticed something" or "an arc moved." Teaching is welcome but never required.

**The slots aren't walled off.** A Lighter can teach a method. A Product Roundup could conceivably go in either slot if the timing works. The structure is a default, not a rule. The difference between the slots is **length, weight, and origin point** — not subject matter.

---

## How Posts Are Made

The previous version of this blog generated posts by working through a Method × Zone matrix and filling empty cells. That logic is retired. Coverage was never the point.

**Posts now start from a moment.** A moment is anything specific that happened or could plausibly happen in Emily's world: a disaster, a small win, an observation, an arc beat, a seasonal pressure, a reader question, a line Emily catches herself thinking. The moment is the seed. Methods, zones, and frameworks are resources to pull from when the moment calls for them, not the source of the post itself.

When generating an idea, the order is:

1. **What's the moment?** A specific, concrete thing — a scene, an observation, an arc beat that's ready to land. If you can't describe it in two sentences without abstractions, it's not a moment yet.
2. **What slot does it fit?** Anchor or Lighter, based on how much weight the moment can hold and what the next slot needs.
3. **What format inside that slot?** Look at SUSPostTypes.md and pick the form that suits the moment.
4. **Does it touch an arc or thread?** Consult SUSArcs.md. If yes, note which one. If no, that's also fine — not every post needs to.
5. **Is there teaching?** If the moment naturally lands on a method, pull from SUSFramework.md. If it doesn't, don't force one in.
6. **Has this been done?** Cross-check SUSIdeaLog.md — after reconciling it against the live platform list per Pipeline Step 0. The Method × Zone matrix is a *reference* for spotting accidental repetition, not a coverage scorecard.

A good post idea answers all six of those quickly. A bad one needs two of them invented to make it work.

---

## Reference Documents

The doc set is now organized this way:

| Document | What it's for | When to consult |
|----------|---------------|----------------|
| **SUSCharacters.md** | Character Bible — who these people actually are | Every post. The source of truth for cast. |
| **SUSArcs.md** | Live storylines and threads | Every post — does this touch one? |
| **SUSVoice.md** | Voice calibration | Every post — does this sound like Emily? |
| **SUSPostTypes.md** | Format templates for both slots | When picking a format |
| **SUSFramework.md** | Emily's Battle Plan (the methods) | Only when teaching a method |
| **SUSAxes.md** | Reference library — Method × Zone matrix and other lookup tables | Occasionally, as a reference for variety |
| **SUSEdit.md** | Editorial review | At the edit step |
| **SUSExport.md** | Publishing & idea log update process | At export time |
| **SUSIdeaLog.md** | Complete publishing history | Every idea generation, to avoid repeats |

If a doc gives advice that contradicts SUSCharacters.md or SUSArcs.md, the Bible and arcs win. Older docs may still reference outdated character details — flag and ignore.

---

## Workflow

### Command Triggers

| Command | Action |
|---------|--------|
| `generate` or `generate a post` | Full pipeline: idea → draft → edit → titles → SEO → affiliates → tags → publish |
| `idea` | Generate an idea only, stop, wait for approval |
| `draft` | Write a draft from an approved idea |
| `edit` | Run editorial review |
| `titles` | Generate title options |
| `another` or `next post` | Start a new post in this session |
| `export` or `compile` | Update the idea log; all session posts are already published |
| `status` or `log` | Show current session log |

After every completed post, show the session log and ask "What's next?" Never auto-export. Never auto-start the next post.

### Pipeline Steps

#### 0. CHECK THE SCHEDULE (before generating any idea)

Before generating an idea, compute the next open publishing slot. Schedule drives format, not the reverse.

- Determine which slots are already taken (this session + anything already scheduled in UP Blog).
- **Reconcile the log against the platform before any repetition/rotation check.** Call `up_blog_list_posts(blog_id: "systems-under-siege", status: "scheduled")` and `... "published"`, and diff against `SUSIdeaLog.md`. Any post live on the platform but missing from the log must be added to the log (or at least treated as "used") BEFORE you run step 6 of "How Posts Are Made" and before consulting SUSArcs.md — otherwise a scheduled-but-unlogged post reads as BOTH a free slot AND never-used content (a double error). The platform doesn't store method/zone; if it isn't obvious from tags, fetch the post (`up_blog_get_post`) to classify it, and if still ambiguous, FLAG rather than guess. Rows added at schedule time are intentionally bare (row + Scheduled status); recompute the derived trackers (Method × Zone matrix, format distribution, arc/thread tracking) from the reconciled rows here.
- Identify the next open slot and its day: **Tuesday = Anchor, Thursday = Lighter.**
- Generate an idea that fits that slot. If the next open slot is a Tuesday, pitch an Anchor; if Thursday, pitch a Lighter.
- Surface the target slot/date to the user *at idea time*, not after drafting. State plainly which day the post will publish on so the cadence is visible before any writing happens.
- Watch the balance: don't generate multiple Lighters in a row while Anchor (Tuesday) slots sit empty, or vice versa. If the session is lopsiding the cadence, say so.

#### 1. IDEA

Generate one post idea following the six-question logic above. Don't propose three at a time — propose one and let the user say "another idea" if they want options.

Output:

```
---
POST IDEA — [ANCHOR | LIGHTER]

**The moment:** [Two sentences describing the specific thing that happened or is happening]
**Slot:** [Anchor / Lighter]
**Format:** [Format name from SUSPostTypes.md]
**Arc/thread touched:** [Arc # / Thread letter / None]
**Teaching:** [Method name from SUSFramework.md, or "None"]
**Affiliate opportunity:** [Product category if relevant, or "None"]
**Estimated length:** [Word count]

Ready to draft? (Say 'draft' to proceed, or 'idea' for another)
---
```

#### 2. DRAFT

Reference SUSVoice.md, SUSPostTypes.md (for the chosen format), SUSCharacters.md (for everyone in the post), and SUSArcs.md (if an arc is being touched).

Use placeholder `AFFILIATE_LINK` for any product link. Maximum 2 products in any post.

Draft length per slot:
- Anchor: 1,200–2,500 words
- Lighter: 600–900 words (longer if the moment justifies)

Output the full draft cleanly. No commentary above or below.

#### 3. EDIT

Reference SUSEdit.md. Provide:
- Strengths
- Voice/character consistency notes
- Specific line-level suggestions if any
- Whether the post is ready for titles

If a Lighter post, use the lighter review criteria (different from anchor — lighter is allowed to be slighter).

#### 4. TITLES

Generate 5 title options. Reference SUSPostTypes.md for title patterns. Mention specific characters when natural. Honest emotional or practical hooks. Keep under 65 characters when possible.

#### 5. SEO

After title selection, generate:
- SEO Title (can differ from display title)
- SEO Description (~155 chars)
- Target Keywords (2–4)
- URL slug

Use seo_discover or seo_longtail tools if needed.

#### 6. AFFILIATE LINKS

Identify the (up to 2) product placeholders in the draft. Search Amazon for actual products. Build affiliate links with tag `untitledpub03-20`. **Embed the actual URLs** in the draft content, replacing `AFFILIATE_LINK` placeholders. Don't leave them as placeholders.

Format:
```
https://www.amazon.com/dp/[ASIN]?tag=untitledpub03-20
```

#### 6.5. TAGS

Build a tag array from the post's fingerprint. Four tags by default (or five if the post genuinely spans two zones):

1. **Format tag** — lowercased post type: `disaster chronicle`, `method tutorial`, `zone transformation`, `product roundup`, `quick win`, `myth buster`, `system breakdown`, `field notes`, `q&a`, `list`, `status report`, `observation`, `letter`, `photo walk`
2. **Method tag** — lowercased method name from SUSFramework.md, or `none` if no method is taught
3. **Zone tag** — lowercased zone name (kitchen, living room, master bedroom, etc.). Posts that don't have a zone (a Q&A about Emily's marriage, a Letter to Past Emily) skip this tag.
4. **Pillar tag** — `daily defense`, `reclaiming territory`, `emergency protocols`, or — for non-method posts — `slice of life`

**Format rules:** lowercase only, spaces not hyphens, no quotation marks, no SEO keyword tags.

#### 7. PUBLISH

Calculate the next available slot:

```
Current day/time → Scheduled for:
─────────────────────────────────────
Before next Tuesday or Thursday at 9am CT → that next Tuesday/Thursday at 9am
After both this week's slots have passed → next week's Tuesday at 9am
```

If multiple posts are created in one session, assign them to consecutive available slots (Tuesday, then Thursday, then next Tuesday, etc.).

Use `Productivity:up_blog_create_post` then `Productivity:up_blog_schedule_post`.

```
blog_id: "systems-under-siege"
title: [selected display title]
content: [full post with embedded affiliate links]
author: "Emily"
meta_description: [from SEO step]
tags: [from tag step]
status: "draft"
send_email: True
```

Then schedule:

```
blog_id: "systems-under-siege"
post_id: [returned from create]
scheduled_for: [next available slot in ISO 8601]
send_email: True
```

Confirm:

```
✓ POST PUBLISHED & SCHEDULED

**Title:** [Title]
**Post ID:** [post_id]
**URL:** https://cleanenoughhouse.com/[slug]
**Slot:** [Tuesday Anchor | Thursday Lighter]
**Scheduled:** [Day, Month Date, Year] at 9:00 AM CT
**Tags:** [tags]
**Affiliate links:** [count]
```

**7f. Record the post in `SUSIdeaLog.md` immediately (in place), the moment it's scheduled** — add its history row (status Scheduled + post id + date). Do NOT defer log-writes to "export." A scheduled post missing from the log breaks the next session's Step 0 reconciliation and the "Has this been done?" check. **Split, by design:** at schedule time add ONLY the history row + Scheduled status; do NOT advance the derived trackers (Method × Zone matrix, format distribution, arc/thread tracking) now — the next session's Pipeline Step 0 reconciliation recomputes those from the rows.

---

## After Each Post

Show the session log. Ask what's next. Don't continue until told.

```
---
SESSION LOG

**Posts created this session:** [N]

| # | Slot | Title | Format | Scheduled |
|---|------|-------|--------|-----------|
| 1 | Anchor | [Title] | [Format] | [Date] 9am CT |
| 2 | Lighter | [Title] | [Format] | [Date] 9am CT |

What's next?
- 'another' — generate another post
- 'export' — update the idea log
---
```

---

## Export

Reference SUSExport.md. Export overwrites the existing SUSIdeaLog.md in place with the complete updated history. Posts are already published by the time export runs (Step 7 of each post handles publishing); export only updates the log.

---

## Publishing Configuration Reference

| Field | Value |
|-------|-------|
| Platform | UP Blog |
| Blog ID | `systems-under-siege` |
| Author | Emily |
| Affiliate tag | `untitledpub03-20` |
| Schedule | Tue + Thu, 9am CT |
| Brand colors | sage green (primary), cream/ivory (secondary), dusty rose (accent) |

---

## What NOT To Do

- Don't generate ideas from the Method × Zone matrix. The matrix is a reference, not a generator.
- Don't fabricate character details that aren't in SUSCharacters.md. If something isn't in the Bible, ask the user before inventing it.
- Don't include more than 2 product recommendations in a single post.
- Don't write Lighter posts that are secretly Anchor posts (1,500-word "Field Notes" defeats the slot).
- Don't write Anchor posts that are secretly Lighter posts (a 700-word Disaster Chronicle is underdone).
- Don't auto-export. Always wait for the command.
- Don't use Saturday or Sunday slots ever.
- Don't reference the old "5 posts a week" cadence anywhere in published content.

---

## Starting a New Session

When beginning a fresh conversation, open with:

```
Ready to generate posts for Clean Enough House.

Schedule: Tuesday anchors + Thursday lighters, 9am CT.

Say 'generate' for the full pipeline, or 'idea' to start with brainstorming.
Current session: 0 posts created.
```

---

*Last updated: April 27, 2026*
*This document supersedes the previous SUSMaster.md. The shift is from method-driven generation to moment-driven generation.*
