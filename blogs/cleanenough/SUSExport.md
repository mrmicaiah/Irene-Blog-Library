# Clean Enough House - Export Process

## Overview

The export process happens when the user says "export" or "compile" after creating one or more posts in a session.

**Key Point:** Posts are published individually during the workflow (Step 7 of each post in SUSMaster.md). By the time the user says "export," all session posts are already scheduled in UP Blog with embedded affiliate links.

**Export generates:** An updated idea log, written directly to `SUSIdeaLog.md` in the repo.

---

## Publishing During Workflow (Step 7 — Per Post)

Each post is published immediately after affiliate links are embedded, as part of the per-post pipeline. This section documents the schedule logic and the create/schedule API calls.

### Calculate Next Available Slot

The blog publishes Tuesdays and Thursdays at 9am CT. No exceptions for other days of the week.

**Schedule Logic:**

```
Current day/time → Scheduled for:
─────────────────────────────────────
Mon → Tue 9am
Tue before 9am → Tue 9am (today)
Tue after 9am → Thu 9am
Wed → Thu 9am
Thu before 9am → Thu 9am (today)
Thu after 9am → Tue 9am (next week)
Fri/Sat/Sun → Tue 9am (next week)
```

**Multiple posts in session:**
- First post: Next available slot per the table above
- Second post: The slot after that (alternating Tue/Thu)
- Third post: The slot after that
- Continue alternating, never landing on a non-Tue/non-Thu day

**Slot assignment by post type:**
- Anchor posts go in the next available **Tuesday** slot
- Lighter posts go in the next available **Thursday** slot
- A session that creates posts of mixed types should slot them accordingly, even if that means the second post is scheduled before the first chronologically (e.g., create an Anchor and a Lighter on the same Monday — the Lighter goes Thursday, the Anchor goes Tuesday).

If a session creates two posts of the same type, the second one rolls forward one full week to the same slot (Anchor today → next Tuesday; another Anchor → the Tuesday after that).

**Timezone format:**
- Central Standard Time (Nov–Mar): `T09:00:00-06:00`
- Central Daylight Time (Mar–Nov): `T09:00:00-05:00`

### Create Post via UP Blog

Use `Productivity:up_blog_create_post` with:

```
blog_id: "systems-under-siege"
title: [Selected display title]
content: [Full post content in Markdown WITH embedded affiliate links]
author: "Emily"
meta_description: [SEO description from SEO step]
tags: [Array of 4-5 tags from tag step]
status: "draft"
send_email: True
```

**CRITICAL — Affiliate Links Must Be Embedded:**

The post content must have actual Amazon URLs embedded as markdown links:

```markdown
**[Large Storage Basket](https://www.amazon.com/dp/B08XYZ123?tag=untitledpub03-20)** ($24) - Lives in the living room...
```

NOT placeholder text like `(AFFILIATE_LINK)`.

### Schedule Post

Use `Productivity:up_blog_schedule_post` with:

```
blog_id: "systems-under-siege"
post_id: [returned from create]
scheduled_for: [Next available Tue or Thu at 9:00 AM CT, ISO 8601]
send_email: True
```

### Confirm Each Post

Output for each post:

```
✓ POST PUBLISHED & SCHEDULED

**Title:** [Title]
**Post ID:** [post_id]
**Slot:** [Tuesday Anchor | Thursday Lighter]
**URL:** https://cleanenoughhouse.com/[slug]
**Scheduled:** [Day, Month Date, Year] at 9:00 AM CT
**Tags:** [tag list]
**Affiliate Links:** [X] products with live Amazon links
```

---

## STEP 1: GENERATE UPDATED IDEA LOG (On Export)

### Create Complete Replacement File

The idea log is NOT a merge — it's a **complete replacement** containing:

1. ALL previously published posts (from existing SUSIdeaLog.md)
2. ALL posts from current session (with scheduled dates)

### File Structure

```markdown
# CLEAN ENOUGH HOUSE - MASTER IDEA LOG
## Last Updated: [Current Date]

---

## COMPLETE POST HISTORY

| # | Date | Slot | Title | Type | Method | Zone | Status |
|---|------|------|-------|------|--------|------|--------|
[All posts in chronological order]

**Total Posts:** [X] ([Y] published, [Z] scheduled)

---

## METHOD × ZONE COVERAGE MATRIX

[Updated matrix showing method/zone combinations covered by Anchor posts]

---

## FORMAT DISTRIBUTION

[Updated counts by post type, separated by Anchor and Lighter]

---

## CHARACTER USAGE

[Updated character tracking — last appearance, frequency]

---

## ARC/THREAD TRACKING

[Which arcs moved, which threads were touched in recent posts]

---

## SESSION HISTORY

[Add new session entry]

---

## NOTES

[Any relevant updates]

---

*This log REPLACES all previous versions.*
*Last updated: [Current Date]*
```

### Output File

Save by overwriting the existing `SUSIdeaLog.md` in the repo, in place.

Write the updated content directly to `SUSIdeaLog.md` in the repo, overwriting the previous version.

---

## STEP 2: SESSION SUMMARY

After generating the idea log, output:

```
---
EXPORT COMPLETE

**Posts Published This Session:** [X]

| # | Slot | Title | Scheduled | Affiliate Links |
|---|------|-------|-----------|-----------------|
| 1 | Anchor | [Title] | [Date] 9am CT | [X] products |
| 2 | Lighter | [Title] | [Date] 9am CT | [X] products |

**Files Generated:**
- SUSIdeaLog.md (updated in place in the repo)

**Next Steps:**
1. The updated SUSIdeaLog.md is now committed in the repo
2. Start next session when ready

Total posts now: [Previous total + Session posts]
---
```

---

## CRITICAL RULES

### Never Auto-Export
- Always wait for the user to explicitly say "export" or "compile"
- After each post, show session log and ask "What's next?"
- User controls when session ends

### Complete Replacement
- Idea log is NOT incremental
- Every export generates a COMPLETE file
- The worker overwrites SUSIdeaLog.md directly in the repo

### Publishing Order
- Posts scheduled in their proper slot (Anchor → Tuesday, Lighter → Thursday)
- Skip non-Tue/non-Thu days automatically
- Never double-book a date

### Required for Each Post
Before a post is considered complete, it must have:
- ✓ Approved idea (with slot identified)
- ✓ Complete draft
- ✓ Edit review passed
- ✓ Title selected
- ✓ SEO metadata generated
- ✓ Affiliate links found and embedded (if any — max 2)
- ✓ Tags built
- ✓ Published and scheduled in UP Blog

---

## Timezone Reference

| Period | Offset | Example |
|--------|--------|---------|
| Standard Time (Nov–Mar) | -06:00 | 2026-01-13T09:00:00-06:00 |
| Daylight Time (Mar–Nov) | -05:00 | 2026-07-14T09:00:00-05:00 |

**DST transitions (approximate):**
- Spring forward: Second Sunday of March
- Fall back: First Sunday of November

---

## Example Session Flow

**Session with 3 posts created on a Monday morning:**

Post 1: Anchor — Disaster Chronicle
→ Affiliate links embedded
→ Published & scheduled for Tuesday 9am CT (this week)

Post 2: Lighter — Field Notes
→ Affiliate links embedded (or none)
→ Published & scheduled for Thursday 9am CT (this week)

Post 3: Anchor — Method Tutorial
→ Affiliate links embedded
→ Published & scheduled for Tuesday 9am CT (next week)

User says "export":
1. Rewrite SUSIdeaLog.md with all entries including the 3 new ones
2. Overwrite SUSIdeaLog.md in the repo
3. Show export summary

By export time, all posts are already live in UP Blog with clickable affiliate links.

---

*Last updated: April 27, 2026*
*This document supersedes the previous SUSExport.md. The major change is the Tuesday + Thursday cadence (replacing the old weekdays-only logic).*
