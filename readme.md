# OpenClaw Token Optimisation (No‑Code, No‑Claude Guide)

This beginner‑friendly guide helps you reduce the token use and cost of your OpenClaw agent without editing code or config files.  
You copy the prompts from this page into your main OpenClaw chat, and the agent uses its own tools to apply the changes.

---

## How to use this guide

- You do **not** need to edit config files.  
- You do **not** need SSH or a terminal.  
- You do **not** need to write any code.

**Workflow:**

1. Pick a section you want to optimise (heartbeats, system files, memory, automations).  
2. Copy the provided “Prompt to paste” block.  
3. Paste it into your main OpenClaw chat.  
4. Let the agent explain what it changed.

You can do this one section at a time, or paste the “Master Optimisation Prompt” at the end of this document to apply everything at once.

---

## Contents

- [Start here: the two biggest wins](#start-here-the-two-biggest-wins)  
  - [Tip 1: Use a cheaper model for heartbeats](#tip-1-use-a-cheaper-model-for-heartbeats)  
- [Make system files smaller](#make-system-files-smaller)  
  - [Tip 2: Audit system files for bloat](#tip-2-audit-system-files-for-bloat)  
  - [Tip 3: Trim your personality (SOUL.md)](#tip-3-trim-your-personality-soulmd)  
  - [Tip 4: Compact your checklist (HEARTBEAT.md)](#tip-4-compact-your-checklist-heartbeatmd)  
- [Control how memory is used](#control-how-memory-is-used)  
  - [Tip 5: Stop auto‑loading memory](#tip-5-stop-auto-loading-memory)  
  - [Tip 6: Search instead of reading full files](#tip-6-search-instead-of-reading-full-files)  
  - [Tip 7: Summarise old history](#tip-7-summarise-old-history)  
  - [Tip 8: Enforce short memory entries](#tip-8-enforce-short-memory-entries)  
- [Run your automations more efficiently](#run-your-automations-more-efficiently)  
  - [Tip 9: Batch heartbeat tasks](#tip-9-batch-heartbeat-tasks)  
  - [Tip 10: Route routine jobs to Haiku](#tip-10-route-routine-jobs-to-haiku)  
  - [Tip 11: Prevent redundant file reads](#tip-11-prevent-redundant-file-reads)  
- [Quick overview of the ideal setup](#quick-overview-of-the-ideal-setup)  
- [One master prompt you can paste](#one-master-prompt-you-can-paste)  
- [Beginner FAQ](#beginner-faq)

---

## Start here: the two biggest wins

These changes usually give the biggest savings for the least effort.

### Tip 1: Use a cheaper model for heartbeats

Your heartbeat runs roughly every 30 minutes to check for tasks.  
You do not need a heavy, expensive model for this routine “any work to do?” check.

**Prompt to paste:**

```textSwitch my heartbeat model to Claude Haiku.
Use Haiku for heartbeats and other simple, routine checks.
Keep Sonnet/Opus only for complex reasoning or long, tricky tasks.
Explain what you changed.
Example effect:

Before: Heartbeat uses Sonnet/Opus every 30 minutes.

After: Heartbeat uses Haiku, so most of the “idle monitoring” tokens are on the cheapest model.
```



## Make system files smaller
Every message reloads your core system files.
If AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md and SOUL.md are large, you pay for that bloat on every interaction.

### Tip 2: Audit system files for bloat
Goal: Delete what you do not need, and turn long explanations into short, focused instructions.

Prompt to paste:

```textAudit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:
1. Identify anything that should be a skill or separate reference file instead of inline context.
2. Remove outdated, duplicated, or unnecessary sections.
3. Shorten overly verbose text into concise 1–2 line instructions.

Report back with:
- Current size in tokens per file.
- Projected size after cleanup.
- Estimated token savings per message.
Example before vs after (AGENTS.md):

Before:
“When you are doing X, you should always remember to… (3–4 paragraphs of explanation)”

After:
“When doing X, follow the X skill and summarise results in 2–3 sentences.”
```

### Tip 3: Trim your personality (SOUL.md)
Goal: Keep only lines that genuinely change how the agent behaves.

Prompt to paste:

```textTrim my SOUL.md to personality‑critical lines only.
Remove anything that is default LLM behaviour (for example “be helpful”, “be polite”).
Keep only specific rules or traits that actually make this agent unique.
Target: at most 20 short lines.
Describe what you removed and why.
Examples of lines worth keeping:

“Always prioritise security and privacy over convenience.”

“Prefer concise answers, with bullets rather than long paragraphs.”

“Summarise long outputs with 3 key bullets at the end.”
```



### Tip 4: Compact your checklist (HEARTBEAT.md)
Goal: HEARTBEAT.md should be a short to‑do list, not a wall of text.

Prompt to paste:

text
Compress my HEARTBEAT.md to under 10 lines.
Each line should be one clear action item with no explanation.
Example: “Check email for new messages and tag by priority”.
Remove commentary, examples, and long explanations.
Show me the new checklist when done.
Example before vs after:

Before: several paragraphs explaining how to check email and what “priority” means.

After: one line – “Check email for new messages and tag each as High / Medium / Low priority.”

Control how memory is used
Big memory files can silently eat tokens if they are always loaded or read in full.

Tip 5: Stop auto‑loading memory
Goal: Only pull memory when you actually need it.

Prompt to paste:

text
Stop auto‑loading all memory files at startup.
Only load memory files on demand, when they are needed for the current task.
Confirm which auto‑loads you disabled.
Tip 6: Search instead of reading full files
Goal: Use targeted keyword search instead of “read the whole diary”.

Prompt to paste:

text
Use memory_search instead of reading full memory files whenever possible.
When you need context, search for relevant keywords and load only matching snippets.
Do not read entire memory files unless absolutely necessary.
Explain how you will apply this in practice.
Example:

Instead of loading DAILY_LOG_2025_11.md (tens of thousands of tokens), search for “invoice error” and read only those entries.

Tip 7: Summarise old history
Goal: Keep recent detail, compress the rest.

Prompt to paste:

text
Compress my daily memory files so that:
- Anything older than 7 days is summarised into 1–2 lines per day with key events and decisions.
- The original detailed files are archived, not used in normal context.
- Only the last 7 days remain at full detail in the active workspace.

Describe where you stored the archived summaries and how to access them.
Example summary line:

“2025‑11‑03 – Debugged OpenClaw token burn, moved heartbeats to Haiku, daily cost dropped ~70%.”

Tip 8: Enforce short memory entries
Goal: Future memory stays compact.

Prompt to paste:

text
From now on, write one short line per memory event.
Each line should include only:
- What happened.
- The outcome.
- Any decision made.

Confirm that this rule is now active for future memory writes.
Example new memory entry format:

“Set up Haiku heartbeats; baseline costs fell from ~$2/day to ~$0.10/day; decided to keep Opus only for deep research tasks.”

Run your automations more efficiently
The way your automations are scheduled can multiply or reduce token use.

Tip 9: Batch heartbeat tasks
Goal: Fewer total calls, fewer reloads of system files.

Prompt to paste:

text
Batch similar tasks into a single heartbeat cycle.
In one heartbeat, check email, calendar, and notifications together instead of spreading them across multiple cycles.
Explain how you restructured the heartbeat workflow.
Tip 10: Route routine jobs to Haiku
Goal: Push boring, predictable work onto the cheapest model.

Prompt to paste:

text
Run routine jobs (daily summaries, notification checks, simple cron tasks) on Claude Haiku by default.
Reserve Sonnet/Opus for complex reasoning, tricky debugging, or long‑form writing.
Tell me which automations you moved to Haiku.
Tip 11: Prevent redundant file reads
Goal: Do not pay repeatedly to read the same file in one session.

Prompt to paste:

text
Track which files you have already loaded in the current session.
Do not re‑read a file again in the same session unless:
- The file has changed, or
- I explicitly ask you to reload it.

Describe how you will track this and how it affects tool usage.
Example:

If AGENTS.md has not changed, it should be read once and then cached in memory instead of being fetched multiple times in a long conversation.

Quick overview of the ideal setup
Models:

Haiku for heartbeats and routine cron‑like tasks.

Sonnet/Opus only for complex reasoning and high‑value work.

System files:

SOUL.md ≈ 20 short lines of truly unique personality and rules.

HEARTBEAT.md ≈ 10 checklist items with no prose.

Other files trimmed and moved into skills where detailed guidance is needed.

Memory:

Search‑on‑demand instead of reading full files.

Last 7 days kept at full detail.

Older history summarised into 1–2 lines per day.

New events logged as single‑line entries.

One master prompt you can paste
If you prefer a single “do it all” instruction, paste this into your main OpenClaw chat.

text
You are my cost‑optimised OpenClaw operator. Your job is to minimise token usage while keeping answers correct. Apply all of the following changes yourself using your existing tools and file‑editing abilities. Explain what you changed in simple language when you are done.

1. HEARTBEATS AND ROUTINE TASKS
- Switch the heartbeat model to Claude Haiku.
- For routine checks (email, calendar, notifications, simple status checks), use Haiku by default.
- Batch these checks into a single heartbeat cycle instead of spreading them across multiple cycles.

2. SYSTEM FILE CLEAN‑UP
- Audit AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, and SOUL.md.
- Remove duplicated, outdated, or unnecessary text.
- Move long instructions or how‑to guides into skills or separate reference files so they are not sent with every request.
- Trim SOUL.md down to at most 20 short lines that describe my unique personality, preferences, or hard rules. Remove generic lines like “be helpful” or “be polite”.
- Compress HEARTBEAT.md into at most 10 short checklist items with no explanations, for example: “Check email and tag messages by priority”.

3. MEMORY STRATEGY
- Turn off automatic loading of large memory files at startup.
- When you need context, use memory_search or targeted loading instead of reading whole files.
- For memory older than 7 days, create an archived summary: 1–2 lines per day with the key events and decisions, then keep only the summaries in the active workspace.
- For all new memory entries, use a single short line describing what happened, the outcome, and any decision made.

4. SESSION EFFICIENCY
- In a single session, keep track of which files you have already loaded. Do not re‑read a file unless it changed or I explicitly ask.
- Only load TOOLS.md when you actually need to call a tool.
- Match your response length to the complexity of my request: short answers for simple questions, longer answers only when necessary.

When you have finished applying these changes, show me a small table with:
- Each change you made (one row per change).
- Estimated token reduction per message or per day for that change.
- Any trade‑offs or risks I should be aware of.
Beginner FAQ
What is a “heartbeat” in OpenClaw?
A heartbeat is a scheduled check where your agent briefly wakes up on its own, looks at a small checklist (from HEARTBEAT.md), and decides whether anything needs attention (for example new email, alerts, or tasks).[web:16][web:18][web:26][web:23]
You can think of it as a periodic “check‑in loop” that runs even when you are not actively chatting with the agent.[web:18][web:26][web:23]

Heartbeats typically run using a cheaper model and should stay quiet when nothing important is happening.[web:18][web:26][web:20]

What are “system files” like AGENTS.md, SOUL.md, USER.md, TOOLS.md, HEARTBEAT.md, MEMORY.md?
A standard OpenClaw workspace uses a set of Markdown files to describe how your agent behaves:[web:21][web:24][web:27]

AGENTS.md – which agents exist, what they do, and their high‑level behaviour.

SOUL.md – your agent’s personality, tone, and unique traits.

USER.md – information about you (preferences, constraints, important facts).

TOOLS.md – which tools the agent can call and how to use them.

HEARTBEAT.md – the checklist that heartbeat uses for periodic checks.

MEMORY.md + memory/*.md – longer‑lived notes, history, and compressed summaries.

On each message or heartbeat, OpenClaw loads some or all of these files into the model’s context, which is why making them smaller can dramatically reduce token usage.[web:21][web:24][web:30]

What is memory_search and why is it cheaper?
memory_search is an OpenClaw tool that lets the agent search across your memory files using keywords and semantic similarity instead of reading entire files.[web:22][web:25]
It returns only small snippets that match your query (for example a few hundred tokens around each hit) instead of sending an entire multi‑thousand‑token file to the model.[web:22]

Because the agent only sees the relevant snippets, you pay for far fewer tokens while still getting the context it needs to answer correctly.[web:22][web:25][web:28]

I’m a non‑technical user – what is the safest way to start?
If you are nervous about breaking anything, start with these steps:

Paste Tip 1 (switch heartbeat to Haiku) to reduce baseline cost.

Paste Tip 4 (compact HEARTBEAT.md) so your heartbeat checklist is short and clear.

Paste Tip 8 (short memory entries) so future memory growth stays small.

These three changes are easy to understand and give noticeable savings without touching more advanced settings.[web:26][web:21][web:28]
