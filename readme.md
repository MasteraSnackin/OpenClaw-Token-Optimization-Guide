# 🚀 OpenClaw Token Optimization Guide: 15 Cost-Cutting Prompts

Maximize your performance while minimizing your API spend. This guide contains 15 direct prompts and operational tips to help you cut OpenClaw costs by up to 60%.

---

## 📖 How to Use This Guide

> [!IMPORTANT]
> **No config editing, no SSH, no code.** Simply copy-paste any prompt below directly to your OpenClaw agent. It will handle the rest.

---

## 📑 Table of Contents

1. [THE BIG TWO (Do These First)](#-the-big-two-do-these-first)
2. [SYSTEM FILE OPTIMIZATION](#%EF%B8%8F-system-file-optimization)
3. [MEMORY MANAGEMENT](#-memory-management)
4. [OPERATIONAL EFFICIENCY](#-operational-efficiency)
5. [SUMMARY: The Optimal Setup](#-summary-the-optimal-setup)
6. [Master Prompt for Your Agent](#-master-prompt-for-your-agent)

---

## 🔥 THE BIG TWO (Do These First)

### TIP 1: Switch Your Heartbeat to a Cheaper Model

Your heartbeat fires every 30 minutes (48x/day). Most of the time, it just checks for updates. You don't need Opus for that.

**Prompt:**

```text
Switch my heartbeat model to Haiku.
```

> [!NOTE]
> **Why it works:** Haiku costs ~95% less than Opus per token. This single change can cut 30-40% of your total daily spend.

### TIP 2: Get the Claude Max Plan

If you use proactive checks, email, or heavy automations, you're likely spending $500–$2,000+/mo on API.

**Action:** Go to [claude.ai/settings](https://claude.ai/settings) and upgrade to **Max ($200/mo)** for unlimited Opus.

> [!TIP]
> **The Math:** $200 flat vs. $1,800+ on API = Instant massive savings.

---

## ⚙️ SYSTEM FILE OPTIMIZATION

*Every message loads your core files. Every unnecessary line costs you every time.*

### TIP 3: Audit System Files for Token Waste

**Prompt:**

```text
Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:
1. What's in here that should be a skill instead of context?
2. What's outdated or redundant?
3. What's too verbose?
Give me the current size, projected size, and estimated token savings.
```

> [!TIP]
> **Expected result:** Most users cut 40-60% of their system file size through this audit.

### TIP 4: Trim SOUL.md to Personality-Critical Lines

**Prompt:**

```text
Trim my SOUL.md to personality-critical lines only. Remove anything that's default model behavior (e.g., "be helpful"). Keep only what makes you unique—specific rules or traits you wouldn't have without being told.
```

### TIP 5: Keep HEARTBEAT.md Under 10 Lines

**Prompt:**

```text
Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove all explanations—just the checklist.
```

---

## 🧠 MEMORY MANAGEMENT

### TIP 6: Only Load Memory Files on Demand

**Prompt:**

```text
Only load memory files on demand. Don't auto-load everything at startup. Pull what you need, when you need it.
```

### TIP 7: Use memory_search Instead of Loading Full Files

**Prompt:**

```text
Use memory_search instead of loading full memory files. When you need context, search for keywords instead of reading the entire file.
```

### TIP 8: Compress Old Memory Files

**Prompt:**

```text
Compress my daily memory files. Summarize anything older than a week into 1-2 lines per day and archive the originals. Keep only the last 7 days at full detail.
```

### TIP 9: Write Shorter Memory Entries

**Prompt:**

```text
Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made.
```

---

## ⚡ OPERATIONAL EFFICIENCY

### TIP 10: Batch Similar Tasks in One Heartbeat

**Prompt:**

```text
Batch similar tasks instead of handling them one at a time. Check email, calendar, and notifications in a single heartbeat cycle instead of spreading them across multiple.
```

### TIP 11: Use Haiku Cron Jobs for Routine Tasks

**Prompt:**

```text
Use cron jobs on Haiku for routine tasks (daily summaries, notification checks) instead of handling them in the main Opus session.
```

### TIP 12: Don't Re-Read Files Already Loaded

**Prompt:**

```text
Don't read files you've already read this session. Track what you've loaded and skip re-reads unless I explicitly ask you to reload something.
```

### TIP 13: Skip TOOLS.md When Tools Aren't Needed

**Prompt:**

```text
Stop loading TOOLS.md if you're not using any tools this interaction. Only pull it in when you actually need tool-specific instructions.
```

### TIP 14: Archive Old Cron Job Outputs

**Prompt:**

```text
Archive old cron job outputs instead of keeping them in the active workspace. Move anything older than 3 days to an archive folder.
```

### TIP 15: Match Response Length to Complexity

**Prompt:**

```text
When I ask a simple question, give me a short answer. Don't write three paragraphs when one sentence works. Match your response length to the complexity of my request.
```

---

## 🎯 SUMMARY: The Optimal Setup

- **Plan:** Claude Max ($200/mo flat) for unlimited Opus.
- **Models:** Heartbeats and routine cron jobs running on **Haiku**.
- **System Files:** Lean files (SOUL.md ~20 lines, HEARTBEAT.md ~10 lines).
- **Memory:** Loaded on demand, compressed weekly, and one-line entries.

---

## 🤖 Master Prompt for Your Agent

Paste this as a single message to your main OpenClaw agent and let it edit its own files and behaviours:

```text
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
```

---

*Generated with ❤️ by MasteraSnackin*
