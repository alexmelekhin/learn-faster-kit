---
name: learn-faster-progress
description: Produce a Learn FASTER progress report from metadata, syllabus, progress logs, and review statistics.
---

# Learn FASTER Progress

Use this skill when the user asks for learning progress, stats, milestones, what to do next, or a summary of a Learn FASTER topic.

## Workflow

1. Inspect `.learning/config.json`. If `.learning/` is missing, tell the user there is no active learning project and suggest `$learn-faster "<topic>"`.
2. Ensure `.learning/scripts/generate_syllabus.py` exists. If helper scripts are missing, copy the bundled scripts from `plugins/learn-faster/skills/learn-faster/scripts/*.py` into `.learning/scripts/`.
3. Identify the topic. If unclear, run:
   `python3 .learning/scripts/generate_syllabus.py list`
   and ask which topic to summarize.
4. Read these files when present:
   - `.learning/<topic-slug>/metadata.json`
   - `.learning/<topic-slug>/progress.md`
   - `.learning/<topic-slug>/syllabus.md`
   - `.learning/<topic-slug>/review_schedule.json`
   - `.learning/<topic-slug>/concepts/*.json`
5. Calculate and report:
   - Session count from `metadata.json`.
   - Days since `created_at`.
   - Syllabus completion from checked and unchecked `- [ ]` / `- [x]` items.
   - Learned concepts from `progress.md`, `review_schedule.json`, and concept JSON files.
   - Review stats: concepts scheduled, total completed reviews, due review count, next review date, and quiz accuracy when available.
   - Next focus: the next 2-3 unchecked syllabus items or weakest concepts.
   - Milestones reached or nearby.
6. Keep the report concise, useful, and grounded in the files. If data is missing, say which metric is unavailable instead of guessing.

## Report Shape

```markdown
## Progress Report: <Topic>

Overview: <sessions>, <days>, <mode/status>
Syllabus: <percent> (<complete>/<total> items)

Learned Concepts
- <concept>

Review Stats
- Scheduled: <count>
- Completed reviews: <count>
- Due now: <count>
- Next review: <date or none>

Next Focus
1. <next item>
2. <next item>

Milestones
- <session/completion/review milestone>
```

## Milestones

- 5 sessions: building momentum.
- 10 sessions: consistent learning habit.
- 25%, 50%, 75%, and 100% syllabus completion.
- First review completed, 10 reviews completed, and no overdue reviews.
- First quiz recorded and 80%+ quiz accuracy when concept quiz data exists.

Suggest `$learn-faster-review` when reviews are due, `$learn-faster-practice` when the next step is applied work, and `$learn-faster` when the next step is new learning.
