# Learn FASTER

[![Python Version](https://img.shields.io/badge/python-3.12+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![uv](https://img.shields.io/endpoint?url=https://raw.githubusercontent.com/astral-sh/uv/main/assets/badge/v0.json)](https://github.com/astral-sh/uv)

Learn FASTER is an AI learning kit for Claude Code and Codex. It creates a
structured learning workspace with personalized syllabi, progress tracking,
spaced repetition, practice exercises, and printable exam generation.

The project is built around the FASTER framework:

- **Forget**: start with a beginner's mindset.
- **Act**: learn by doing, not by passively reading.
- **State**: manage focus, energy, and difficulty.
- **Teach**: explain concepts in your own words to retain them.
- **Enter**: keep a consistent learning cadence.
- **Review**: use spaced repetition for long-term retention.

## Contents

- [What You Get](#what-you-get)
- [Install](#install)
- [Claude Code Workflow](#claude-code-workflow)
- [Codex Workflow](#codex-workflow)
- [CLI Reference](#cli-reference)
- [Learning Modes](#learning-modes)
- [Exam PDFs](#exam-pdfs)
- [Teach-Back Example](#teach-back-example)
- [Development](#development)
- [Requirements](#requirements)
- [Use Cases](#use-cases)
- [Contributing](#contributing)
- [Attribution](#attribution)
- [License](#license)

## What You Get

- Personalized syllabi for the topic, mode, and goal.
- Five learning modes: Balanced, Exam-Prep, Theory-Focused, Practical, and
  Programming.
- Spaced repetition with review scheduling in `.learning/`.
- Progress reports from session logs, syllabus completion, and review stats.
- Practice exercises and mini-projects.
- Printable exams, answer keys, and optional PDFs.
- Separate Claude Code slash commands and Codex skills.

## Install

Learn FASTER requires Python 3.12+ and
[uv](https://docs.astral.sh/uv/).

Install `uv` if needed:

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Install Learn FASTER once and use it across projects:

```bash
uv tool install learn-faster --from git+https://github.com/alexmelekhin/learn-faster-kit.git
```

For one-time use without a persistent tool install:

```bash
uvx --from git+https://github.com/alexmelekhin/learn-faster-kit.git learn-faster
```

After installation, choose the workflow for your AI coding environment.

## Claude Code Workflow

Use this path when you want Claude Code slash commands such as `/learn`,
`/review`, and `/progress`.

### Claude Code Setup

From the project where you want to learn:

```bash
cd your-learning-project
learn-faster
```

On first run, the CLI:

- asks you to choose a learning mode;
- creates `.claude/` commands and agents;
- creates `.learning/` tracking files and helper scripts;
- writes `CLAUDE.md` when it does not already exist;
- launches Claude Code with the Learn FASTER coaching prompt.

### Claude Code Commands

- `/learn [topic]`: start or continue a topic with a personalized syllabus.
- `/review`: run a spaced-repetition review session.
- `/progress`: show sessions, syllabus progress, concepts, and review stats.

### Claude Code Files

The Claude Code setup creates this structure:

```text
your-project/
|-- .claude/
|   |-- agents/
|   |   `-- practice-creator.md
|   |-- commands/
|   |   |-- learn.md
|   |   |-- review.md
|   |   `-- progress.md
|   `-- settings.local.json
|-- .learning/
|   |-- config.json
|   |-- references/
|   |   `-- faster_framework.md
|   `-- scripts/
|       |-- concept_quiz.py
|       |-- generate_exam_pdf.py
|       |-- generate_syllabus.py
|       |-- init_learning.py
|       |-- log_progress.py
|       `-- review_scheduler.py
`-- CLAUDE.md
```

### Claude Code Daily Flow

1. Run `/learn "Topic"` to create or continue a topic.
2. Complete due `/review` items before new material.
3. Learn one small concept at a time.
4. Teach the concept back in your own words.
5. Log progress and add new concepts to review.
6. Run `/progress` to see what to focus on next.

## Codex Workflow

Use this path when you want a repo-local Codex plugin with `$learn-faster`
skills.

### Codex Setup

From the project where you want the local plugin:

```bash
cd your-learning-project
learn-faster codex-init
```

Then open Codex from that repository and enable Learn FASTER from `/plugins`.

### Codex Skills

- `$learn-faster [topic]`: start or continue learning with syllabus,
  review, and progress tracking.
- `$learn-faster-review`: run an explicit spaced-repetition review session.
- `$learn-faster-progress`: show sessions, syllabus completion, learned
  concepts, review stats, next focus, and milestones.
- `$learn-faster-practice`: generate exercises, drills, and mini-projects.
- `$learn-faster-exam`: generate printable exams, answer keys, and PDFs.

### Codex Files

The Codex setup creates this structure:

```text
your-project/
|-- .agents/
|   `-- plugins/
|       `-- marketplace.json
`-- plugins/
    `-- learn-faster/
        |-- .codex-plugin/
        |   `-- plugin.json
        `-- skills/
            |-- learn-faster/
            |-- learn-faster-exam/
            |-- learn-faster-practice/
            |-- learn-faster-progress/
            `-- learn-faster-review/
```

The first learning session also creates the shared `.learning/` workspace.
That workspace remains compatible with the Claude Code workflow.

### Codex Daily Flow

1. Use `$learn-faster "Topic"` to create or continue a topic.
2. Use `$learn-faster-review` when reviews are due or when you want recall
   practice.
3. Use `$learn-faster-practice` after learning concepts that need applied
   reinforcement.
4. Use `$learn-faster-progress` to decide the next focus.
5. Use `$learn-faster-exam` when you want a printable mock exam.

## CLI Reference

- `learn-faster`: auto-initialize and launch Claude Code in coach mode.
- `learn-faster init`: force re-initialization or switch learning modes.
- `learn-faster codex-init`: install the repo-local Codex plugin and
  marketplace entry.
- `learn-faster exam-pdf <markdown-path>`: generate a PDF from an exam
  Markdown file using the installed package environment.
- `learn-faster version`: show the installed version.

## Learning Modes

Choose the mode that fits the learning goal:

- **Balanced**: mix theory, practice, and application.
- **Exam-Prep**: focus on recall, timed drills, mock exams, and weak areas.
- **Theory-Focused**: build mental models, first principles, and conceptual
  clarity.
- **Practical**: learn by building useful projects immediately.
- **Programming**: learn programming through implementation, debugging,
  tests, and code review.

Each mode changes the coaching style, syllabus shape, and practice strategy.

## Exam PDFs

Exam mode can create Markdown exam papers and answer keys. To convert an exam
Markdown file to PDF, use:

```bash
learn-faster exam-pdf exam/exam-topic-20260430.md
```

When using only the copied helper script outside the package environment, use:

```bash
uv run --with reportlab python3 .learning/scripts/generate_exam_pdf.py exam/exam-topic-20260430.md
```

If ReportLab is unavailable, the helper script writes a printable HTML fallback
and reports that a PDF was not produced.

## Teach-Back Example

The "T" in FASTER is teach-back. The coach asks you to explain the idea instead
of only reading an answer.

```bash
mkdir learn-go
cd learn-go
learn-faster
/learn "Go error handling"
```

Example session:

```text
Coach: You just learned about error wrapping. Can you explain the key idea
in your own words?

You: When I wrap an error with fmt.Errorf and %w, I add context while keeping
the original error in the chain. errors.Is can still match the root cause.

Coach: That captures the important part. I will add "error wrapping" to your
review schedule so it comes back tomorrow.
```

Teach-back forces active recall, which improves retention compared with passive
reading. The goal is not just to receive an answer. The goal is to reconstruct
the idea clearly enough that you can explain and apply it later.

## Development

Clone the repository and install dependencies:

```bash
git clone https://github.com/alexmelekhin/learn-faster-kit.git
cd learn-faster-kit
uv sync
```

Useful checks:

```bash
uv lock --check
uv run --locked ruff check
python3 -m compileall -q src/learn_faster plugins/learn-faster/skills/learn-faster/scripts
```

## Requirements

- Python 3.12+
- uv
- Claude Code or Codex

## Use Cases

Learn FASTER is useful for:

- learning programming languages such as Go, Rust, Python, and TypeScript;
- preparing for technical certifications and exams;
- mastering frameworks and libraries;
- building structured self-study programs;
- onboarding to new codebases or technologies.

## Contributing

Contributions are welcome. Open an issue or pull request with the problem,
proposed change, and any relevant workflow details.

## Attribution

This project is a fork of Hugo Lau's Learn FASTER kit:
<https://github.com/cheukyin175/learn-faster-kit>.

## License

MIT License. See [LICENSE](LICENSE) for details.
