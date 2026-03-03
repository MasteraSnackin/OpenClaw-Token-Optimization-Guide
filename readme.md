# OpenClaw Token Optimisation Guide

15 Easy Ways to Cut Your AI Costs

---

## Quick Start: Highest‑Impact Prompts

If you only do a few things, start with these:

**1. Switch Heartbeat to Haiku**

> Switch my heartbeat model to Haiku.

**2. Shorten HEARTBEAT.md**

> Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove any explanations — just the checklist.

**3. Shorter Answers**

> When I ask a simple question, give me a short answer. Don’t write three paragraphs when one sentence works. Match your response length to the complexity of the question.

**4. Shorter Memory Entries**

> Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made.

**5. Audit System Files**

> Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:  
> (1) What’s in here that should be a skill instead of always‑loaded context  
> (2) What’s outdated or redundant  
> (3) What’s too verbose and could say the same thing in fewer words  
>  
> Give me the current size, projected size after cleanup, and estimated token savings.

---

## How to Use This Guide

- This guide is written for beginners.  
- You do not need to write code, touch config files, or use SSH.  
- Each tip has a Prompt block.  
- To apply a tip, simply:
  1. Open your OpenClaw chat.
  2. Copy the entire Prompt block (including all lines).
  3. Paste it into the chat and send.
  4. Let OpenClaw confirm what it changed.

You can use the tips in any order, but beginners should start with:

- TIP 1 (short answers)  
- TIP 2 (shorter memory)  
- TIP 3 (short heartbeat)  
- TIP 4 and TIP 5 (cheaper models)  

---

## Contents

- [Start With Easy Wins](#start-with-easy-wins)  
  - [TIP 1: Match Response Length to Question Complexity](#tip-1-match-response-length-to-question-complexity)  
  - [TIP 2: Write Shorter Memory Entries](#tip-2-write-shorter-memory-entries)  
  - [TIP 3: Keep `HEARTBEAT.md` Under 10 Lines](#tip-3-keep-heartbeatmd-under-10-lines)  

- [Cut Background Waste](#cut-background-waste)  
  - [TIP 4: Switch Your Heartbeat to a Cheaper Model](#tip-4-switch-your-heartbeat-to-a-cheaper-model)  
  - [TIP 5: Use Haiku Cron Jobs for Routine Tasks](#tip-5-use-haiku-cron-jobs-for-routine-tasks)  
  - [TIP 6: Batch Similar Tasks in One Heartbeat](#tip-6-batch-similar-tasks-in-one-heartbeat)  

- [Fix System Files](#fix-system-files)  
  - [TIP 7: Trim `SOUL.md` to Personality‑Critical Lines Only](#tip-7-trim-soulmd-to-personalitycritical-lines-only)  
  - [TIP 8: Audit Your System Files for Token Waste](#tip-8-audit-your-system-files-for-token-waste)  
  - [TIP 9: Skip `TOOLS.md` When You Don’t Need Tools](#tip-9-skip-toolsmd-when-you-dont-need-tools)  

- [Make Memory Cheaper](#make-memory-cheaper)  
  - [TIP 10: Only Load Memory Files on Demand](#tip-10-only-load-memory-files-on-demand)  
  - [TIP 11: Use `memory_search` Instead of Loading Full Files](#tip-11-use-memory_search-instead-of-loading-full-files)  
  - [TIP 12: Compress Old Memory Files](#tip-12-compress-old-memory-files)  

- [Clean Up How Sessions Run](#clean-up-how-sessions-run)  
  - [TIP 13: Don’t Re‑Read Files You’ve Already Loaded](#tip-13-dont-re-read-files-youve-already-loaded)  
  - [TIP 14: Archive Old Cron Job Outputs](#tip-14-archive-old-cron-job-outputs)  

- [The Big Plan Change](#the-big-plan-change)  
  - [TIP 15: Get the Claude Max Plan](#tip-15-get-the-claude-max-plan)  

- [FAQ for Beginners](#faq-for-beginners)  

- [Ideal Beginner‑Friendly Setup](#ideal-beginnerfriendly-setup)  

---

## Start With Easy Wins

### TIP 1: Match Response Length to Question Complexity

Long answers cost more. Simple questions rarely need more than one sentence.

**Prompt:**

> When I ask a simple question, give me a short answer. Don’t write three paragraphs when one sentence works. Match your response length to the complexity of the question.

---

### TIP 2: Write Shorter Memory Entries

Verbose memories become expensive to reload later. One short line per event is enough.

**Prompt:**

> Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made.

---

### TIP 3: Keep `HEARTBEAT.md` Under 10 Lines

Your heartbeat runs many times per day. A big `HEARTBEAT.md` wastes tokens repeatedly.

**Prompt:**

> Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove any explanations — just the checklist.

---

## Cut Background Waste

### TIP 4: Switch Your Heartbeat to a Cheaper Model

Heartbeats mostly check for work and do nothing. They don’t need your most powerful (and most expensive) model.

**Prompt:**

> Switch my heartbeat model to Haiku.

Why it works: Haiku is much cheaper per token than Opus, but it can still follow a simple checklist just fine.

---

### TIP 5: Use Haiku Cron Jobs for Routine Tasks

Cron jobs run in separate sessions and often do routine checks. These don’t need Opus either.

**Prompt:**

> Use cron jobs on Haiku for routine tasks instead of handling them in the main Opus session. Daily summaries, notification checks, and routine monitoring should all run on cheaper models.

---

### TIP 6: Batch Similar Tasks in One Heartbeat

If OpenClaw checks email, calendar, and notifications in separate heartbeats, it reloads context each time. That multiplies cost.

**Prompt:**

> Batch similar tasks instead of handling them one at a time. Check email, calendar, and notifications in a single heartbeat cycle instead of spreading them across multiple.

---

## Fix System Files

### TIP 7: Trim `SOUL.md` to Personality‑Critical Lines Only

Most `SOUL.md` files repeat generic behaviour the model already has. Those lines cost tokens every single request.

**Prompt:**

> Trim my SOUL.md to personality‑critical lines only. Remove anything that’s default model behaviour. Keep only what makes you YOU — unique personality traits, specific rules, things you wouldn’t do without being told.

---

### TIP 8: Audit Your System Files for Token Waste

Files like `SOUL.md`, `USER.md`, `TOOLS.md`, and `HEARTBEAT.md` are loaded again and again. Anything unnecessary in them burns money every time.

**Prompt:**

> Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:  
> (1) What’s in here that should be a skill instead of always‑loaded context  
> (2) What’s outdated or redundant  
> (3) What’s too verbose and could say the same thing in fewer words  
>  
> Give me the current size, projected size after cleanup, and estimated token savings.

---

### TIP 9: Skip `TOOLS.md` When You Don’t Need Tools

`TOOLS.md` only matters when tools are in use. For normal conversation it’s just extra, costly context.

**Prompt:**

> Stop loading TOOLS.md if you’re not using any tools this interaction. Only pull it in when you actually need tool‑specific instructions.

---

## Make Memory Cheaper

### TIP 10: Only Load Memory Files on Demand

Loading all memory files at startup front‑loads cost before you even talk to the AI.

**Prompt:**

> Only load memory files on demand. Don’t auto‑load everything at startup. Pull what you need, when you need it.

---

### TIP 11: Use `memory_search` Instead of Loading Full Files

Reading an entire `MEMORY.md` file every time is overkill. Searching for specific terms is much cheaper.

**Prompt:**

> Use memory_search instead of loading full memory files. When you need context about something, search for it instead of reading the whole file.

---

### TIP 12: Compress Old Memory Files

Details from weeks ago rarely need full text. Summaries keep context small and cheap.

**Prompt:**

> Compress my daily memory files. Summarise anything older than a week into 1–2 lines per day and archive the originals. Keep the last 7 days at full detail.

---

## Clean Up How Sessions Run

### TIP 13: Don’t Re‑Read Files You’ve Already Loaded

If a file is already loaded in this session, reading it again wastes tokens.

**Prompt:**

> Don’t read files you’ve already read this session. Track what you’ve loaded and skip re‑reads unless I explicitly ask you to reload something.

---

### TIP 14: Archive Old Cron Job Outputs

Old cron outputs clutter the workspace and may get scanned during operations, adding extra tokens.

**Prompt:**

> Archive old cron job outputs instead of keeping them in active workspace. Move anything older than 3 days to an archive folder.

---

## The Big Plan Change

### TIP 15: Get the Claude Max Plan

If you’re using OpenClaw heavily via API, you can easily spend hundreds or thousands per month in usage fees. A flat‑fee Max plan can be much cheaper.

**Action:**

Go to `claude.ai/settings` and upgrade to **Max 20x** (`$200`/month).

---

## FAQ for Beginners

### What is a heartbeat?

A heartbeat is a scheduled check your OpenClaw agent runs automatically (for example every 15–30 minutes) to see if anything needs attention without you sending a message first.[web:34]  
On each heartbeat, it reads `HEARTBEAT.md`, follows a short checklist (like “check email” or “look for urgent alerts”), and then either does nothing or takes action if it finds work.[web:37]

---

### What is a system file?

A system file is a markdown file in your OpenClaw workspace that defines how your agent behaves, who you are, and what tools it can use.[web:32][web:35]  
Common system files include:  
- `SOUL.md` – the agent’s personality, boundaries, and tone.[web:32][web:35]  
- `USER.md` – details about you (name, timezone, preferences).[web:32][web:35]  
- `TOOLS.md` – instructions and definitions for tools the agent can call.[web:32]  
- `HEARTBEAT.md` – the checklist the agent follows on each heartbeat.[web:32][web:34]  

These files are often loaded into context every time the agent runs, which is why keeping them short saves tokens.[web:38]

---

### What is `memory_search`?

`memory_search` is a built‑in OpenClaw tool that lets your agent search across your memory markdown files (like `MEMORY.md` and `memory/*.md`) using natural‑language queries.[web:33][web:39]  
Instead of loading full files, it searches small chunks and returns only the most relevant snippets, which gives the agent the context it needs while using far fewer tokens.[web:33][web:39]

---

### Why do shorter files and answers save money?

OpenClaw pays for both input tokens (what it reads) and output tokens (what it writes), so large system files and long replies cost more every time the agent runs.[web:8][web:26]  
By trimming system files, using `memory_search`, and keeping answers concise, you reduce the number of tokens processed per run, which directly lowers your bill.[web:8][web:11]

---

### Do I need to edit files manually to use this guide?

No. Every change in this guide can be triggered by copy‑pasting the provided prompts into your OpenClaw chat and letting the agent update files for you.[web:21]  
Manual file editing is optional; beginners can rely entirely on the prompts until they are comfortable making direct edits.

---

## Ideal Beginner‑Friendly Setup

1. Use Claude Max if your monthly usage is high.  
2. Run heartbeats and cron jobs on Haiku.  
3. Keep `SOUL.md` and `HEARTBEAT.md` short and focused.  
4. Load memory only when needed and use `memory_search`.  
5. Keep responses and memories concise so fewer tokens are used each time.
