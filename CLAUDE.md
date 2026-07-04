# Irene-Blog-Library

A blog-writing engine for three blogs. A manager (a separate Claude, running in a claude.ai project) dispatches you — a Claude Code worker in this repo — to write posts. When dispatched, you'll be told which blog to write for. This file tells you how to execute.

## The three blogs

The three blogs DO NOT share a workflow. Each has its own pipeline defined in its Master. Do not assume what works for one applies to another.

| Blog | Slug / folder | Prefix | Distinctive workflow |
|------|---------------|--------|----------------------|
| Hot Mess (thehotmesscoffeeshop.com) | blogs/hotmess/ | hm | Leanest. Pre-generation check, then IDEA to DRAFT to EDIT to TITLES to EXPORT. Fiction (Rena LeeAnn, a coffee shop). No SEO, no interview. |
| Clean Enough House (cleanenoughhouse.com) | blogs/cleanenough/ | SUS | Opens with a SCHEDULE CHECK (schedule drives format), then IDEA to DRAFT to EDIT to TITLES to SEO to affiliates to tags to PUBLISH. Fiction (Emily, WFH mom). Has affiliate/tag steps the others lack. |
| Irene D (irenegdaniels.com) | blogs/irene/ | igd | Only blog that INTERVIEWS. SEO DISCOVER to IDEA to INTERVIEW to DRAFT to EDIT to TITLES to EXPORT. Interview happens before drafting; the draft is built from the answers. KJV Scripture only. |

## How to write a post (once you've been assigned a blog)

1. Read the blog's folder, starting with [prefix]Instructions.md, then [prefix]Master.md. The Master is authoritative on THIS blog's pipeline, including steps the other blogs don't have (Clean Enough's schedule check and affiliate/tag steps; Irene's SEO discovery and interview). Then read the other files in the folder as the Master directs (voice, characters, world, post types, edit rules, log).
2. Read the log BEFORE generating. You start with no memory of prior posts. The blog's log ([prefix]StoryLog.md or [prefix]IdeaLog.md) tells you what's been written, what's due, and what to avoid repeating. Read it first, every time.
3. Honor the blog-specific first step, then STOP for topic approval — do NOT proceed to drafting on your own. Hot Mess and Clean Enough (the entertainment blogs): after the pre-generation check (Clean Enough: schedule check), report TOPIC OPTIONS for the user to choose from — the slot/date, what's blocked/overdue, and 2-4 rotation-legal options each with story type, a one-line premise, character(s), and theme, plus your recommendation. Then WAIT for the user to pick. Draft only the option the user selects. Irene: run SEO discovery (unless told "skip seo"), then INTERVIEW the user before drafting — do not draft from assumptions. In every case, drafting begins only after the user has approved a topic (or, for Irene, answered the interview).

## The review-and-publish flow (CRITICAL)

- Draft first, to the review folder, NOT the repo. Write your draft as a plain-text .txt file to:
  /Users/tulipsworkhorse/Documents/Claude/Projects/blog library/draft/
  Name it clearly, e.g. hotmess-draft-[short-title].txt. This is the user's reading copy. Do NOT commit drafts to the repo.
- Stop after the draft. Report it's ready. Do NOT publish. The user must review and approve first.
- On approval (which comes as a SEPARATE dispatch): write the final post as markdown into the repo, publish per the blog's Export doc ([prefix]Export.md), and update the blog's log IN PLACE (overwrite the existing log, never create a new dated file).
- Publishing uses the up_blog_* tools (via the Productivity MCP; load them when needed). Each blog's Export doc specifies its blog_id and schedule.

## Hard rules
- Never publish without an explicit approval dispatch. Drafting and publishing are separate steps with a human gate between them.
- Logs are updated in place: overwrite [prefix]StoryLog.md / [prefix]IdeaLog.md, never spawn a dated copy.
- Clean Enough House's blog_id is systems-under-siege: correct and load-bearing; do not "fix" it despite the display name being Clean Enough House.
- You cannot git push: the harness denies it. Commit your work; the user pushes from their terminal.
- One post per dispatch. Multiple blogs means multiple separate dispatches.

## Current focus
_Updated at the end of each session._

Setup complete: three blogs migrated to blogs/, stale Claude-projects/download/PDF/compile-to-document language removed, per-blog Instructions files created, Clean Enough display name scrubbed (blog_id retained), encoding mojibake fixed, routing doc written. NEXT: run a live test — dispatch a worker to write a test Hot Mess post and confirm the engine executes end to end.
