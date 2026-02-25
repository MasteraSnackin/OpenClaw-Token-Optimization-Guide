
15 Prompts & Tips to Cut Your Costs


How to use this guide: Copy-paste any prompt below directly to your OpenClaw. No config editing, no SSH, no code. Just message your AI and it handles the rest.


THE BIG TWO (Do These First)

TIP 1: Switch Your Heartbeat to a Cheaper Model

Your heartbeat fires every 30 minutes. That's 48 times a day. Most of the time, it checks a file and says "nothing to do." You don't need your most expensive model for that.

Prompt:
Switch my heartbeat model to Haiku.

Why it works: Haiku costs ~95% less than Opus per token. It can read a checklist and decide if something needs attention just fine. This single change can cut 30-40% of your daily spend.


TIP 2: Get the Claude Max Plan

If you're on API and actually using your OpenClaw (proactive checks, email, calendar, automations), you're likely spending $500-2,000+/mo. The Max plan is $200/mo flat for unlimited Opus.

The math: $200 flat vs. $1,800+ on API = instant savings. This is the single biggest cost move you can make.

Action: Go to claude.ai/settings and upgrade to Max 20x ($200/mo).


SYSTEM FILE OPTIMIZATION

TIP 3: Audit Your System Files for Token Waste

Every time your OpenClaw responds, it loads SOUL.md, USER.md, TOOLS.md, and HEARTBEAT.md. Every unnecessary line costs tokens on every single message, heartbeat, and cron job.

Prompt:
Audit every file that loads into your context each message (AGENTS.md, TOOLS.md, USER.md, MEMORY.md, HEARTBEAT.md, SOUL.md). For each one:

(1) What's in here that should be a skill instead of always-loaded context
(2) What's outdated or redundant
(3) What's too verbose and could say the same thing in fewer words

Give me the current size, projected size after cleanup, and estimated token savings.



Expected result: Most people cut 40-60% of their system files. That compounds on every interaction.


TIP 4: Trim SOUL.md to Personality-Critical Lines Only

Half the instructions in most SOUL.md files are things the model already does. "Be helpful." "Be conversational." "Respond clearly." The model does that by default. You're paying for instructions that change nothing.

Prompt:
Trim my SOUL.md to personality-critical lines only. Remove anything that's default model behavior. Keep only what makes you YOU — unique personality traits, specific rules, things you wouldn't do without being told.

Tip: A tight SOUL.md is 15-30 lines. If yours is 100+, it's costing you.


TIP 5: Keep HEARTBEAT.md Under 10 Lines

Your heartbeat file loads every 30 minutes. If it's a wall of text, you're burning tokens 48 times a day on instructions that could be three bullet points.

Prompt:
Compress my HEARTBEAT.md to under 10 lines. Each line should be one clear action item. Remove any explanations — just the checklist.


MEMORY MANAGEMENT

TIP 6: Only Load Memory Files on Demand

By default, your OpenClaw might read today's memory, yesterday's memory, and MEMORY.md on every session start. That's a lot of tokens before a single word is exchanged.

Prompt:
Only load memory files on demand. Don't auto-load everything at startup. Pull what you need, when you need it.


TIP 7: Use memory_search Instead of Loading Full Files

Instead of reading your entire MEMORY.md every time it needs context, your OpenClaw can search for specific keywords. Targeted retrieval vs. loading everything.

Prompt:
Use memory_search instead of loading full memory files. When you need context about something, search for it instead of reading the whole file.


TIP 8: Compress Old Memory Files

Daily memory files grow forever. Entries from two weeks ago rarely need full detail. A summary keeps the context at a fraction of the token cost.

Prompt:
Compress my daily memory files. Summarize anything older than a week into 1-2 lines per day and archive the originals. Keep the last 7 days at full detail.


TIP 9: Write Shorter Memory Entries

Your OpenClaw tends to write verbose memories. A paragraph per event means more tokens to load later. One line per event is enough.

Prompt:
Write shorter memory entries going forward. One line per event, not a paragraph. Include only: what happened, the result, and any decision made.


OPERATIONAL EFFICIENCY

TIP 10: Batch Similar Tasks in One Heartbeat

If your OpenClaw checks email, then calendar, then notifications in three separate heartbeats, that's three full context loads. Batching them into one cycle saves two full loads.

Prompt:
Batch similar tasks instead of handling them one at a time. Check email, calendar, and notifications in a single heartbeat cycle instead of spreading them across multiple.


TIP 11: Use Haiku Cron Jobs for Routine Tasks

Cron jobs run in isolated sessions. Routine checks, daily summaries, and notification scans don't need Opus. Run them on Haiku and save Opus for conversations that matter.

Prompt:
Use cron jobs on Haiku for routine tasks instead of handling them in the main Opus session. Daily summaries, notification checks, and routine monitoring should all run on cheaper models.


TIP 12: Don't Re-Read Files You've Already Loaded

If your OpenClaw loaded SOUL.md at the start of a conversation, it doesn't need to read it again mid-conversation. Simple but surprisingly common waste.

Prompt:
Don't read files you've already read this session. Track what you've loaded and skip re-reads unless I explicitly ask you to reload something.


TIP 13: Skip TOOLS.md When You Don't Need Tools

TOOLS.md is context that only matters when your OpenClaw uses a tool. For casual conversation, it's dead weight sitting in context.

Prompt:
Stop loading TOOLS.md if you're not using any tools this interaction. Only pull it in when you actually need tool-specific instructions.

Note: This depends on your OpenClaw setup. Some configurations auto-inject TOOLS.md. If so, keep it short.


TIP 14: Archive Old Cron Job Outputs

Old outputs pile up in your workspace. Your OpenClaw might scan them during file operations, wasting tokens on stale data.

Prompt:
Archive old cron job outputs instead of keeping them in active workspace. Move anything older than 3 days to an archive folder.


TIP 15: Match Response Length to Question Complexity

Output tokens cost money too. When you ask "what time is my next call?" you don't need three paragraphs. Tell your OpenClaw to be concise by default.

Prompt:
When I ask a simple question, give me a short answer. Don't write three paragraphs when one sentence works. Match your response length to the complexity of the question.


PUTTING IT ALL TOGETHER

The optimal setup:
1. Claude Max plan ($200/mo flat) for unlimited Opus
2. Heartbeats and routine cron jobs on Haiku
3. Lean system files (SOUL.md ~20 lines, HEARTBEAT.md ~10 lines)
4. Memory loaded on demand, not at startup
5. Short memory entries, compressed weekly
