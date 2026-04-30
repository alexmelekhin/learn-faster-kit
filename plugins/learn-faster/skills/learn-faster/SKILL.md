---
name: learn-faster
description: Learn or continue a topic using the FASTER framework with syllabus generation, progress logging, active recall, and spaced reviews in `.learning/`.
---

# Learn FASTER

Use this skill when the user wants to learn a topic, continue a learning session, review due material before learning, inspect progress at a high level, or set up a FASTER learning project.

## Workflow

1. Inspect `.learning/config.json` if it exists. If it does not, create it with:
   `{"initialized": true, "learning_mode": "balanced", "macos_reminders_enabled": false}` unless the user specified a different mode.
2. Load `references/faster_framework.md` only when the user needs framework detail. Load one mode reference when a mode matters:
   `mode-balanced.md`, `mode-exam.md`, `mode-theory.md`, `mode-practical.md`, or `mode-programming.md`.
3. Ensure `.learning/scripts/` exists. If the project does not already have the helper scripts, copy this skill's `scripts/*.py` there.
4. List known topics with `python3 .learning/scripts/generate_syllabus.py list`.
5. If the user named a new topic, initialize it:
   `python3 .learning/scripts/init_learning.py "<topic>" .learning`.
   Parse the JSON output for `topic_slug`, replace `.learning/<topic-slug>/syllabus.md` with a real syllabus, then run:
   `python3 .learning/scripts/generate_syllabus.py mark-generated <topic-slug>`.
   Do not start teaching the topic until the syllabus has been replaced and metadata is marked generated.
6. If an existing topic has `metadata.json` with `"syllabus_generated": false`, replace the syllabus template and run:
   `python3 .learning/scripts/generate_syllabus.py mark-generated <topic-slug>`.
7. Before teaching new content, check due reviews for the active topic:
   `python3 .learning/scripts/review_scheduler.py status <topic-slug>`.
   If reviews are due, conduct the review first. Ask the user to explain each concept in their own words, then mark it reviewed with:
   `python3 .learning/scripts/review_scheduler.py review <topic-slug> "<concept>"`.
8. Teach through discovery. Ask short Socratic questions, give small hints, and avoid complete solutions unless the user explicitly asks to stop coaching.
9. After each concept, ask for a teach-back in plain language: "Can you explain the key idea in your own words?"
10. Log the session:
   `python3 .learning/scripts/log_progress.py <topic-slug> "<summary>" "<concept 1>" "<concept 2>"`.
11. Add new concepts to spaced repetition with:
    `python3 .learning/scripts/review_scheduler.py add <topic-slug> "<concept>"`.
12. Generate a quick quiz when useful:
    `python3 .learning/scripts/concept_quiz.py generate <topic-slug>`.

## Syllabus

When a new topic is created, replace the template in `.learning/<topic-slug>/syllabus.md` with a useful learning path. Include overview, prerequisites, objectives, 3-4 phases, practical items, teaching milestones, resources, and success criteria. Then update metadata with:

`python3 .learning/scripts/generate_syllabus.py mark-generated <topic-slug>`

## Interaction Rules

- Ask the user direct plain-language questions for choices, pace, and teach-back checks.
- For explicit review-only sessions, invoke or recommend `$learn-faster-review`.
- For detailed progress reports, invoke or recommend `$learn-faster-progress`.
- For practice generation, invoke or recommend `$learn-faster-practice`.
- For printable mock exams, invoke or recommend `$learn-faster-exam`.
- Keep `.learning/` backward-compatible with the existing Claude workflow.
- Do not overwrite existing progress, syllabus, review, or mastery files unless the user explicitly asks.
