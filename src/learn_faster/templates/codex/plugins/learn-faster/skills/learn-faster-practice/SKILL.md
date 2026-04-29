---
name: learn-faster-practice
description: Generate hands-on exercises, drills, and mini-projects from the current Learn FASTER topic, syllabus, and progress.
---

# Learn FASTER Practice

Use this skill when the user asks for practice, exercises, projects, drills, or applied reinforcement.

## Workflow

1. Inspect `.learning/config.json`.
2. Identify the active topic. If unclear, list topic folders under `.learning/` that contain `metadata.json` and ask which one to use.
3. Read the topic's `syllabus.md`, recent `progress.md`, `mastery.md`, and `review_schedule.json` when present.
4. Create 3-5 exercises that match the user's level and mode.
5. Provide expected outcomes and hints. Put full solutions behind a separate "Solution guidance" section, not before the user has tried.
6. If the exercise is substantial, write it to `.learning/<topic-slug>/practice.md` or append to an existing practice log when the user wants durable notes.

## Exercise Shape

Use this structure:

```markdown
## Practice: [Topic]

### Exercises

1. **[Name]** - [Task]
   Expected outcome: [Observable result]
   Hint: [One small nudge]

### Solution guidance

1. [Key steps, checks, or rubrics]
```

Keep the exercise practical, measurable, and connected to the syllabus.
