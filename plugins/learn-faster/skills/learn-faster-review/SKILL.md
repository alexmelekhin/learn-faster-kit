---
name: learn-faster-review
description: Run a spaced-repetition review session for Learn FASTER topics using `.learning/<topic>/review_schedule.json`.
---

# Learn FASTER Review

Use this skill when the user asks to review, recall, refresh, or practice due Learn FASTER concepts.

## Workflow

1. Inspect `.learning/config.json`. If `.learning/` is missing, tell the user there is no active learning project and suggest `$learn-faster "<topic>"`.
2. Ensure `.learning/scripts/review_scheduler.py` exists. If helper scripts are missing, copy the bundled scripts from `plugins/learn-faster/skills/learn-faster/scripts/*.py` into `.learning/scripts/`.
3. Identify the topic. If unclear, run:
   `python3 .learning/scripts/generate_syllabus.py list`
   and ask which topic to review.
4. Check due reviews:
   `python3 .learning/scripts/review_scheduler.py status <topic-slug>`.
5. If no reviews are due, summarize the next scheduled review dates from `.learning/<topic-slug>/review_schedule.json` and offer to continue learning with `$learn-faster`.
6. If reviews are due, review one concept at a time:
   - Ask the user to explain the concept from memory.
   - Use short hints before giving an explanation.
   - Ask one follow-up question when the explanation is partial.
   - Mark the concept reviewed only after the user has attempted recall:
     `python3 .learning/scripts/review_scheduler.py review <topic-slug> "<concept>"`.
7. If the user cannot recall a concept after hints, briefly reteach it, ask for a corrected teach-back, then mark it reviewed. Add a narrower remedial concept with `review_scheduler.py add` only when a specific gap needs its own review.
8. After the review session, report reviewed count, any difficult concepts, next review dates, and a concise next step: learn new material with `$learn-faster`, practice with `$learn-faster-practice`, or stop for today.

## Review Style

- Prioritize active recall over recognition.
- Keep prompts short and direct.
- Do not answer before the user has tried.
- Use the user's explanation to diagnose gaps.
- Keep `.learning/` files compatible with the Claude `/review` workflow.
