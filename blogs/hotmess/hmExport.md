# THE HOT MESS — EXPORT PROCESS

## CRITICAL RULE

**NEVER AUTO-EXPORT.**

Export happens ONLY when the user explicitly says:
- "export"
- "publish"
- "schedule"
- "post"
- "done"
- "that's all"

After every completed story, always ask: **"another or export?"**

---

## WHAT EXPORT MEANS

**Export = Publish to The Hot Mess blog**

Stories are published directly to `the-hot-mess` blog via the UP Blog tools, scheduled at **8:00 AM Central Time** on three days per week:

| Day | Slot Type | Story Type Pool |
|-----|-----------|-----------------|
| Tuesday | Anchor | Day, Incident, Visitor, Portrait, Milestone, Flashback |
| Friday | Anchor | Day, Incident, Visitor, Portrait, Milestone, Flashback |
| Sunday | Flex | Quiet, Letter, Moment |

**Stories must match their slot type.** An Incident cannot go on Sunday. A Quiet cannot go on Tuesday or Friday.

---

## WORKFLOW

### After Each Story Completion

Display:

```
## STORY COMPLETE ✓

**Session Log:**
| # | Title | Slot | Type | Character | Theme | Words |
|---|-------|------|------|-----------|-------|-------|
| 1 | [Title] | [Tue/Fri/Sun] | [Type] | [Character] | [Theme] | [Count] |

**What's next?**
- Say **"another"** to generate another story
- Say **"export"** to schedule stories for publication
```

### If User Says "Another"
Loop back to idea generation. **Determine which slot is needed next** based on what's already in the session and what slots remain unfilled in the upcoming week.

### If User Says "Export"
Proceed with publishing process below.

---

## PUBLISHING PROCESS

### Step 1: Determine Slots for Each Story

For each story in the session, identify its required slot:
- **Anchor types** (Day, Incident, Visitor, Portrait, Milestone, Flashback) → Tuesday or Friday
- **Flex types** (Quiet, Letter, Moment) → Sunday

### Step 2: Map Stories to Calendar

Find the next available slots, in order, that match each story's type.

**Calendar logic:**
- Today's date is known
- The next slots are: next Tuesday, next Friday, next Sunday (whichever come first chronologically)
- For each story, take the next available slot that matches its type
- If no future-dated correct-type slot exists in the immediate week, push to the following week

**Example:** Today is Monday. Session has 1 Visitor + 1 Quiet + 1 Incident.
- Visitor (anchor) → Tuesday this week
- Quiet (flex) → Sunday this week
- Incident (anchor) → Friday this week

**Example:** Today is Wednesday. Session has 2 Anchors + 1 Flex.
- Anchor 1 → Friday this week
- Flex → Sunday this week
- Anchor 2 → Tuesday next week

**Example:** Today is Tuesday after 8 AM CT. Session has 1 Anchor.
- Anchor → Friday this week (Tuesday's slot has passed)

### Step 3: Pre-Publish Summary

Display:

```
## PUBLISH CONFIRMATION

**Stories to schedule:** [X]

| # | Title | Type | Slot | Scheduled For | Words |
|---|-------|------|------|---------------|-------|
| 1 | [Title] | [Type] | [Day] | [Date] 8:00 AM CT | [Count] |
| 2 | [Title] | [Type] | [Day] | [Date] 8:00 AM CT | [Count] |
| 3 | [Title] | [Type] | [Day] | [Date] 8:00 AM CT | [Count] |

**Total word count:** [X]

Ready to schedule? (yes / no)
```

### Step 4: Create Blog Posts

For each story, use `up_blog_create_post`:

```
Tool: up_blog_create_post
Parameters:
  blog_id: "the-hot-mess"
  title: [Approved story title]
  content: [Full story in Markdown]
  tags: [Character names, theme, relevant tags]
  status: "draft"
```

**Content Formatting:**
- Use Markdown format
- Footnotes as `[^1]`, `[^2]`, etc.
- Scene breaks as `---`
- Italics for internal thoughts: `*thought*`
- No HTML needed

**Tag Suggestions:**
- Primary character (e.g., "Todd", "Jennifer", "Walter")
- Theme (e.g., "trust", "community", "courage")
- Story type (e.g., "flashback", "quiet")
- Slot tag (e.g., "tuesday", "sunday") — useful for analytics later
- Recurring elements (e.g., "Betsy", "coffee", "family")

### Step 5: Schedule Posts

For each created post, use `up_blog_schedule_post`:

```
Tool: up_blog_schedule_post
Parameters:
  blog_id: "the-hot-mess"
  post_id: [ID from create step]
  scheduled_for: [ISO 8601 datetime]
  send_email: true
```

**Time Zone Conversion (8:00 AM Central → UTC):**

| Central Time | UTC | Period |
|--------------|-----|--------|
| 8:00 AM CST | 14:00:00Z | November – March |
| 8:00 AM CDT | 13:00:00Z | March – November |

**Example ISO formats:**
- `2026-02-03T14:00:00Z` (CST)
- `2026-07-15T13:00:00Z` (CDT)

### Step 6: Confirm Publication

After scheduling all posts:

```
## EXPORT COMPLETE ✓

**Scheduled for The Hot Mess:**

| # | Title | Slot | Post ID | Scheduled |
|---|-------|------|---------|-----------|
| 1 | [Title] | Tuesday | [ID] | [Date] at 8:00 AM CT |
| 2 | [Title] | Friday | [ID] | [Date] at 8:00 AM CT |
| 3 | [Title] | Sunday | [ID] | [Date] at 8:00 AM CT |

**Email notifications:** Will send to subscribers on publish

**Session stats:**
- Stories: [X]
- Words: [X]
- Themes: [List]
- Characters: [List]

Ready to start a new session anytime!
```

---

## STORY LOG UPDATE

After publishing, generate story log entries for tracking:

**New Entries Format:**

```
| [Date] | [Slot] | [Title] | [Type] | [Character] | [Location] | [Conflict] | [Tone] | [Theme] | [Words] | [Fingerprint] |
```

**Fingerprint Format:**
`[Slot]-[Type]-[Character]-[Location]-[Conflict]-[Tone]-[Theme]`

Examples:
- `Tue-Incident-Todd-HotMess-Operational-Chaotic-Trust`
- `Sun-Quiet-Walter-CornerTable-Internal-Peaceful-Rest`
- `Fri-Portrait-Patricia-CornerTable-Internal-Bittersweet-Love`

---

## CONTINUITY UPDATE

After publishing, note any continuity items for `hmContinuity.md`:

- New character appearances
- Timeline events
- Callbacks established
- Relationship developments
- New running motifs
- Seasonal markers

---

## EDGE CASES

### User Wants to Export Mid-Story
If user says "export" before a story is complete:
```
The current story isn't finished yet. Would you like to:
1. Finish this story first, then publish all
2. Discard the current story and publish completed ones only
3. Save the current draft for later and publish what's done
```

### User Wants Specific Stories Only
If user wants to publish only some stories:
```
Which stories would you like to publish?

| # | Title | Type | Slot |
|---|-------|------|------|
| 1 | [Title] | [Type] | [Day] |
| 2 | [Title] | [Type] | [Day] |

Enter numbers (e.g., "1, 3") or "all"
```

### Slot Mismatch
If a session has 3 anchor stories and 0 flex stories:
- Schedule 2 anchors for Tue + Fri this week
- Sunday slot stays empty (no flex story to fill it)
- Remaining anchor → next Tuesday
- Inform user: "Sunday slot will be unfilled this week — no flex-type story in the session."

If a session has 3 flex stories and 0 anchors:
- Schedule 1 flex for upcoming Sunday
- Remaining 2 flex → next 2 Sundays
- Inform user: "Tuesday and Friday slots will be unfilled — no anchor-type stories in the session."

### Single Story Session
If only one story was created:
```
## EXPORT COMPLETE ✓

**Scheduled for The Hot Mess:**
- "[Title]" → [Day], [Date] at 8:00 AM CT

Email notification will send to subscribers on publish.

Ready for another session anytime!
```

### User Wants Immediate Publish
If user says "publish now" or "post immediately":
- Use `up_blog_publish_post` instead of `up_blog_schedule_post`
- Confirm before publishing: "This will publish immediately and send emails. Proceed?"
- Note: Publishing immediately bypasses the slot system. Use sparingly.

### Scheduling Conflict
Before scheduling, call `up_blog_list_posts` with `status: "scheduled"` to check for existing scheduled posts.
- If a slot is already taken, push to the next available correct-type slot
- Inform user of the adjusted date

### Past-Time Slot
If today's slot has already passed (e.g., it's 9:00 AM Tuesday Central):
- Skip Tuesday's slot for this week
- Move to next available correct-type slot
- Don't try to schedule for a time in the past

---

## TOOL REFERENCE

### up_blog_create_post
Creates a draft post.

| Parameter | Required | Description |
|-----------|----------|-------------|
| blog_id | Yes | `"the-hot-mess"` |
| title | Yes | Story title |
| content | Yes | Full story (Markdown) |
| tags | No | Array of tags |
| status | No | `"draft"` (default) |

### up_blog_schedule_post
Schedules a draft for future publication.

| Parameter | Required | Description |
|-----------|----------|-------------|
| blog_id | Yes | `"the-hot-mess"` |
| post_id | Yes | ID from create step |
| scheduled_for | Yes | ISO 8601 datetime (UTC) |
| send_email | No | `true` (default) |

### up_blog_publish_post
Publishes immediately. Bypasses slot scheduling.

| Parameter | Required | Description |
|-----------|----------|-------------|
| blog_id | Yes | `"the-hot-mess"` |
| post_id | Yes | ID from create step |
| send_email | No | `true` (default) |

### up_blog_list_posts
Check existing posts and schedules. **Always run before scheduling to avoid conflicts.**

| Parameter | Required | Description |
|-----------|----------|-------------|
| blog_id | Yes | `"the-hot-mess"` |
| status | No | `"draft"`, `"scheduled"`, `"published"` |
| limit | No | Number of posts to return |

---

## REMEMBER

1. **Never auto-export** — always ask
2. **Export = Publish** — stories go directly to the blog
3. **Three slots per week** — Tue, Fri, Sun, all at 8:00 AM Central
4. **Slot matches type** — Anchor stories on Tue/Fri only, Flex stories on Sun only
5. **Email notifications on** — subscribers get notified
6. **Update the story log** — tracking enables rotation rules
7. **Note continuity items** — the world builds over time
8. **Confirm before publishing** — no accidents

---

*Export is the finish line. Match the slot. Schedule it. Ship it.*
