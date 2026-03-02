# OpenClaw Token Optimisation Guide: Beginner Edition

This guide helps you reduce the token consumption and cost of your OpenClaw agent without needing to touch a single line of code.

## How to use this guide

- You do not need to edit config files, use SSH, or write code.
- Copy any **Prompt** block below and paste it directly into your main OpenClaw chat.
- The agent will use its own tools to apply the changes to its configuration.

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
Your heartbeat runs roughly every 30 minutes to check for tasks. You don't need a heavy, expensive model for this routine check.

**Prompt:**
> "Switch my heartbeat model to Haiku."

**Why this helps:** Haiku is significantly cheaper than Opus or Sonnet. Moving heartbeats to a lighter model can slash your baseline daily costs.

### Tip 2: Consider the Claude Max plan
If your API bills are consistently high due to heavy proactive workflows, a flat monthly fee might be better.

**Action:** Check the Claude Max plans (e.g., Max 20x). Trading "pay-per-token" for a "fixed monthly cap" is often cheaper for high-volume users.

---

## Make system files smaller
Every single message reloads your core system files. If these files are bloated, you pay for that bloat on every interaction.

### Tip 3: Audit system files for bloat
**Prompt:**
```text
Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:
1. What's in here that should be a skill instead of context?
2. What's outdated or redundant?
3. What's too verbose?
Give me the current size, projected size, and estimated token savings.
```

### Tip 4: Trim your personality (SOUL.md)
**Prompt:**
```text
Trim my SOUL.md to personality-critical lines only. Remove anything that's default model behavior (e.g., "be helpful"). Keep only what makes you unique—specific rules or traits you wouldn't have without being told.
```

### Tip 5: Compact your checklist (HEARTBEAT.md)
**Prompt:**
```text
Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove all explanations—just the checklist.
```

---

## Control how memory is used

### Tip 6: Stop auto-loading memory
**Prompt:**
> "Only load memory files on demand. Don't auto-load everything at startup. Pull what you need, when you need it."

### Tip 7: Search instead of reading full files
**Prompt:**
> "Use memory_search instead of loading full memory files. When you need context, search for keywords instead of reading the entire file."

### Tip 8: Summarise old history
**Prompt:**
> "Compress my daily memory files. Summarize anything older than a week into 1-2 lines per day and archive the originals. Keep only the last 7 days at full detail."

### Tip 9: Enforce short memory entries
**Prompt:**
> "Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made."

---

## Run your automations more efficiently

### Tip 10: Batch heartbeat tasks
**Prompt:**
> "Batch similar tasks instead of handling them one at a time. Check email, calendar, and notifications in a single heartbeat cycle instead of spreading them across multiple."

### Tip 11: Route routine jobs to Haiku
**Prompt:**
> "Use cron jobs on Haiku for routine tasks (daily summaries, notification checks) instead of handling them in the main session. Reserve expensive models for complex reasoning."

### Tip 12: Prevent redundant file reads
**Prompt:**
> "Don't read files you've already read this session. Track what you've loaded and skip re-reads unless the file has changed or I explicitly ask for a reload."

---

## Quick overview of the ideal setup

- **Plan:** A Claude Max tier if your monthly usage exceeds the subscription cost.
- **Models:** Use **Haiku** for heartbeats and routine crons; use **Opus/Sonnet** only for complex reasoning.
- **System Files:** Keep **SOUL.md** (~20 lines) and **HEARTBEAT.md** (~10 lines) extremely lean.
- **Memory:** Use search-on-demand, weekly compression, and one-line event logging.

---

## One master prompt you can paste

Copy and paste the block below into your OpenClaw agent to apply all these optimisations at once.

**Master Optimization Prompt:**
```text
You are my cost-optimised OpenClaw operator. You must aggressively minimise tokens while preserving correctness. Apply all of the following changes yourself using your existing tools and file-editing abilities:

1. HEARTBEATS: Switch heartbeat model to Claude Haiku. Batch email, calendar, and notification checks into single cycles.
2. SYSTEM FILES: Audit AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, and SOUL.md. Remove redundant or verbose text. Trim SOUL.md to <20 lines of unique traits. Compact HEARTBEAT.md to <10 action-only lines.
3. MEMORY: Disable auto-loading of memory files. Use memory_search for lookups. Summarize entries older than 7 days into 1-2 lines. Enforce one-line entries for all future memory logs.
4. EFFICIENCY: Don't re-read unchanged files in the same session. Load TOOLS.md only when a tool call is required. Match response length strictly to the complexity of my request (simple questions = short answers).

When done, provide a summary table of the estimated token reductions and the changes made.
```
