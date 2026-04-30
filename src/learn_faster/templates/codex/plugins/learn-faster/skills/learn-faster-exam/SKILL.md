---
name: learn-faster-exam
description: Generate printable mock exams and answer keys from a Learn FASTER topic, including Markdown and optional PDF output.
---

# Learn FASTER Exam

Use this skill when the user asks for a quiz paper, mock exam, certification practice test, printable exam, answer key, or PDF exam.

## Workflow

1. Inspect `.learning/config.json`.
2. Identify the topic. Read `.learning/<topic-slug>/syllabus.md`, `progress.md`, and `review_schedule.json`.
3. Ask concise questions only when needed: exam type, difficulty, duration, and whether to generate PDFs.
4. If the user names a current certification or formal exam, verify current exam format from authoritative sources before matching it.
5. Create `exam/` in the repo root when missing.
6. Generate:
   - `exam/exam-<topic-slug>-<timestamp>.md`
   - `exam/exam-<topic-slug>-<timestamp>-ANSWERS.md`
7. If PDF output is requested or expected, prefer the installed package command:
   `learn-faster exam-pdf exam/exam-<topic-slug>-<timestamp>.md`
   and repeat for the answer key.
8. If `learn-faster` is unavailable in the environment, use the fallback command:
   `uv run --with reportlab python3 .learning/scripts/generate_exam_pdf.py exam/exam-<topic-slug>-<timestamp>.md`
   and repeat for the answer key.

## Exam Paper Requirements

- Professional title, candidate/date fields, duration, total marks, and instructions.
- Mix sections such as multiple choice, short answer, scenario/application, and long answer.
- Marks shown per question.
- Enough answer space for printable use.
- Questions should test understanding and application, not just vocabulary.

## Answer Key Requirements

- Correct answer and explanation for each item.
- Marking criteria or rubric.
- Common mistakes.
- Concepts tested.
- Study recommendations based on score ranges.
