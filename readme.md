# OpenClaw Token Optimisation Guide: Beginner Edition

---

## How to use this guide

- You do not need to edit config files, use SSH, or write code.  
- Copy any prompt block and paste it into your main OpenClaw agent.  
- The agent should handle the changes itself.

---

## Contents

1. [Start here: the two biggest wins](#start-here-the-two-biggest-wins)  
2. [Make system files smaller](#make-system-files-smaller)  
3. [Control how memory is used](#control-how-memory-is-used)  
4. [Run your automations more efficiently](#run-your-automations-more-efficiently)  
5. [Quick overview of the ideal setup](#quick-overview-of-the-ideal-setup)  
6. [One master prompt you can paste](#one-master-prompt-you-can-paste)

---

## Start here: the two biggest wins

### Tip 1: Use a cheaper model for heartbeats

Your heartbeat runs roughly every 30 minutes and usually just checks for changes. You do not need the most expensive model for that.

**Prompt:**

```text
Switch my heartbeat model to Haiku.
Why this helps: Haiku is much cheaper per token than Opus (roughly an order of magnitude cheaper on typical API pricing), so moving heartbeats to Haiku can remove a large chunk of your daily cost.

Tip 2: Consider the Claude Max plan
If you do a lot of proactive checks, email processing, or heavy workflows, your API bill can easily reach hundreds or thousands per month.

Action:
Go to Claude settings and check the Max plans (for example, Max 20x at around $200/month) to see if a flat monthly fee is cheaper than your current usage.

You are trading “pay per token” for “fixed monthly cap”, which is usually better if your usage is high and predictable.

Make system files smaller
Every message reloads your core files, so long, repetitive files cost you on every single interaction.

Tip 3: Ask the agent to audit your system files
Prompt:

text
Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:
1. What's in here that should be a skill instead of context?
2. What's outdated or redundant?
3. What's too verbose?
Give me the current size, projected size, and estimated token savings.
Typical result: many people can shrink their system files by 40–60% with one pass like this.

Tip 4: Cut SOUL.md down to what really matters
Prompt:

text
Trim my SOUL.md to personality-critical lines only. Remove anything that's default model behavior (e.g., "be helpful"). Keep only what makes you unique—specific rules or traits you wouldn't have without being told.
Aim for a short list of rules that genuinely change how the agent behaves, not general niceness or obvious instructions.

Tip 5: Keep HEARTBEAT.md short
Prompt:

text
Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove all explanations—just the checklist.
This keeps every heartbeat cheap while still telling the agent exactly what to do.

Control how memory is used
Tip 6: Stop loading all memory by default
Prompt:

text
Only load memory files on demand. Don't auto-load everything at startup. Pull what you need, when you need it.
This avoids paying to read big memory files when the current task does not need them.

Tip 7: Use searches instead of loading full memory files
Prompt:

text
Use memory_search instead of loading full memory files. When you need context, search for keywords instead of reading the entire file.
The agent should do targeted lookups instead of always pulling in entire histories.

Tip 8: Summarise old memory
Prompt:

text
Compress my daily memory files. Summarize anything older than a week into 1-2 lines per day and archive the originals. Keep only the last 7 days at full detail.
You keep the important decisions while cutting the token cost of old logs.

Tip 9: Keep new memory entries short
Prompt:

text
Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made.
Short, structured entries are easier to search and cheaper to reload later.

Run your automations more efficiently
Tip 10: Batch work in each heartbeat
Prompt:

text
Batch similar tasks instead of handling them one at a time. Check email, calendar, and notifications in a single heartbeat cycle instead of spreading them across multiple.
One slightly larger heartbeat is cheaper than several separate ones.

Tip 11: Use Haiku for routine cron jobs
Prompt:

text
Use cron jobs on Haiku for routine tasks (daily summaries, notification checks) instead of handling them in the main Opus session.
Reserve expensive models for complex reasoning or higher‑risk actions.

Tip 12: Avoid re-reading the same files
Prompt:

text
Don't read files you've already read this session. Track what you've loaded and skip re-reads unless I explicitly ask you to reload something.
If the file has not changed, re-reading it is pure waste.

Tip 13: Only load TOOLS.md when needed
Prompt:

text
Stop loading TOOLS.md if you're not using any tools this interaction. Only pull it in when you actually need tool-specific instructions.
Many interactions use no tools, so TOOLS.md can stay out of context by default.

Tip 14: Archive old cron outputs
Prompt:

text
Archive old cron job outputs instead of keeping them in the active workspace. Move anything older than 3 days to an archive folder.
This reduces clutter and stops large stale files from being pulled into context.

Tip 15: Keep answers as short as the question
Prompt:

text
When I ask a simple question, give me a short answer. Don't write three paragraphs when one sentence works. Match your response length to the complexity of my request.
This cuts tokens and makes the assistant easier to work with.

Quick overview of the ideal setup
Plan: a Claude Max tier (for example, Max 20x at about $200/month) if it works out cheaper than your current monthly API usage.

Models: heartbeats and routine cron jobs on Haiku; only use Opus/Sonnet when you clearly need more reasoning power.

System files: short SOUL.md (around 20 lines) and HEARTBEAT.md (around 10 checklist lines).

Memory: loaded only when needed, compressed weekly, with one‑line entries for new events.

One master prompt you can paste
Paste this into your main OpenClaw agent. It tells the agent to optimise itself for lower token usage while staying correct.

text
You are my cost-optimised OpenClaw operator. You must aggressively minimise tokens while preserving correctness. Apply all of the following changes yourself using your existing tools and file-editing abilities. If any step fails, report why and skip gracefully instead of retry-looping.

### Heartbeat and plans

- Switch my heartbeat model to Claude Haiku instead of Opus or Sonnet.
- Keep the existing 30-minute cadence unless my current config forces something else.
- For routine cron-style work (daily summaries, notification checks, low-risk monitoring), prefer Haiku or another cheap model where available.
- Only escalate to Opus/Sonnet when you can clearly explain why a cheaper model is insufficient for that specific task.

### System file optimisation

Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each file:

- Identify content that should be a skill or separate file loaded on demand instead of always-on context.
- Remove or rewrite anything outdated, redundant, or obviously verbose.
- Where possible, compress sections into short bullet points or checklists.
- Trim SOUL.md down to only personality-critical lines: keep rules or traits that are genuinely unique to this workspace, remove generic behaviour like "be helpful" or "be polite". Target ~20 lines total.
- Rewrite HEARTBEAT.md so it is under 10 lines, each one a single clear action item with no explanations, prose, or background commentary.
- After changes, tell me for each core file: current size in tokens, previous size if known, and an estimated per-message token reduction.

### Memory management

- Stop auto-loading big memory files at startup. Only load memory files on demand, when they are clearly needed to answer the current request or perform a specific task.
- When you need past context, use memory_search or equivalent targeted lookup instead of reading entire files. Search by relevant keywords, then load only the hits or small excerpts.
- Compress daily memory older than 7 days into 1-2 lines per day (what happened, the outcome, and any key decisions). Archive the originals into an "archive" folder that is not auto-loaded.
- For future entries, write one line per event, not paragraphs. Include only: what happened, the result, and any decision made.

### Operational efficiency

- Batch similar tasks into a single heartbeat where safe: email checks, calendar checks, DMs/notifications, simple status pings should run in one combined cycle rather than separate calls.
- Prefer Haiku for these batched heartbeats and routine cron jobs. Only bring Opus/Sonnet into the loop when there is complex reasoning, high-risk actions, or multi-step planning.
- Do not re-read files you have already loaded in the current session unless I explicitly ask you to reload or you detect that the file has changed on disk. Track what is already in context.
- Do not load TOOLS.md when you are not actually going to use tools in this interaction. Load it only when a tool call is required or imminent.
- Move cron job outputs older than 3 days out of any active workspace or "hot" directory, into an archive location that is never pulled into normal context automatically.

### Response-length discipline

Match your response length strictly to the complexity of my request:

- Simple questions: one short direct answer, optionally a single bullet list if truly necessary.
- Medium tasks: a short explanation plus a concise list of steps or changes.
- Only for genuinely complex, multi-step tasks may you produce a longer, structured answer.
- Default to concise answers and only expand when I explicitly ask for more detail.

### Budget awareness

Add this to your core operating rules:

- Assume I care about keeping monthly LLM spend low.
- Prefer: local/free models (if configured) → cheap models (Haiku) → mid-tier (Sonnet) → Opus only when strictly necessary.
- When you anticipate a very large or multi-turn operation, briefly state your rough token estimate and model choice and wait for my confirmation before proceeding.
- If you notice that projected weekly cost is trending much higher than the past week, proactively suggest concrete configuration or behaviour changes instead of silently continuing.

### When done

- Print a compact summary table of what you changed (file sizes before/after where available, heartbeat model, memory policy, batching rules).
- Mention any steps you could not complete because of missing permissions, missing tools, or constraints in this environment.
