# Irene Grace Daniels Export Process
## Publishing to irenegdaniels.com/blog

---

## OVERVIEW

Export publishes posts directly to irenegdaniels.com/blog using the up_blog_create_post tool with blog_id: "irenegdaniels".

Export is triggered ONLY when Irene explicitly says "export", "publish", or "done". NEVER auto-export after a single post.

---

## TRIGGER CONDITIONS

Export ONLY when Irene says: export, publish, done, finish, wrap up, post it, send it

Do NOT export when a single post is complete. Show session log and ask "another or export" instead.

---

## POST-COMPLETION PROMPT

After EVERY completed post (title selected), show the session log and ask:

**Whats next?**
- Say **"another"** to generate another post  
- Say **"export"** to publish all posts to irenegdaniels.com/blog

NEVER proceed to export without explicit request.

---

## EXPORT PROCESS

### Step 1: Confirm Session Summary
Show all posts and total SEO spend. Get confirmation to proceed.

### Step 2: For Each Post, Ask Publishing Preference
1. **Draft** — Save to blog as draft
2. **Publish now** — Go live immediately  
3. **Schedule** — Set a future publish date/time

Then ask: Send email notification to subscribers? (yes/no)

### Step 3: Publish Using up_blog_create_post

Tool: up_blog_create_post

Parameters:
- blog_id: "irenegdaniels"
- title: [Selected title]
- content: [Full post content in Markdown]
- meta_description: [~155 char SEO description]
- tags: [Array based on pillar and topic]
- status: "draft" OR "published"
- scheduled_for: [ISO datetime if scheduling]
- send_email: true OR false
- author: "Irene G. Daniels"

### Step 4: Report Results
Show status, post ID, and email notification status for each post.

### Step 5: Final Summary
Show all posts published with their status and remaining SEO balance.

---

## TAGS MAPPING

| Pillar | Default Tags |
|--------|--------------|
| The Real | faith, real-life, honesty |
| The Word | scripture, bible, devotional |
| The Grace | grace, freedom, identity |
| The Behind | writing, author-life |
| The Light | joy, humor, celebration |

---

## CRITICAL RULES

1. NEVER auto-export
2. Ask about email notifications
3. Confirm before publishing
4. Track Post IDs
5. Report SEO balance
6. Use blog_id: "irenegdaniels"

