# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2026-04-30

### Added

- Repo-local Codex plugin with bundled `$learn-faster`, `$learn-faster-review`, `$learn-faster-progress`, `$learn-faster-practice`, and `$learn-faster-exam` skills
- Local Codex marketplace entry for discovering the Learn FASTER plugin from this repo
- `learn-faster codex-init` command to install the Codex plugin and marketplace files into another project
- `learn-faster exam-pdf <markdown-path>` command for PDF generation from the installed package environment
- Packaged Codex plugin templates so Codex setup ships with the Python package
- Printable exam generation workflow for exam mode, including answer keys and optional PDF output
- Programming mode for learning programming through project-based approach
- Project-focused practice-creator agent for programming mode
- Programming-specific system prompt and learn command

### Changed

- Documented Claude Code and Codex workflows in the README
- Updated README, package metadata, and plugin metadata to point at `alexmelekhin/learn-faster-kit`
- Aligned the runtime `__version__` with `pyproject.toml` at `2.0.0`
- Simplified practice-creator agents for balanced and practical modes
- Reduced verbosity in practice templates

### Fixed

- Removed stale `.learning/<topic>/progress.json` references from exam-generation guidance
- Made concept quiz generation fall back to `review_schedule.json` when concept metadata files do not exist
- Mirrored review scheduler concepts into `.learning/<topic>/concepts/*.json` for quiz compatibility
- Replaced Codex-facing Claude-only interaction examples with plain user prompts
- Fixed Codex skill metadata to use `policy.allow_implicit_invocation`
- Added deterministic `generate_syllabus.py mark-generated <topic-slug>` metadata updates
- Updated standalone PDF fallback guidance to use `uv run --with reportlab`
- Lazy-loaded the interactive `inquirer` dependency so non-interactive CLI commands can run from source

## [1.1.0] - 2025-11-11

### Features

- **Personalized Learning Modes**: Added four distinct learning modes with tailored experiences
  - **Balanced Mode**: Mix of theory, practice, and application (default)
  - **Exam-Oriented Mode**: Focus on recall, practice tests, and certification prep
  - **Theory-Focused Mode**: Deep conceptual understanding and mental models
  - **Practical Mode**: Build projects immediately, learn by doing
- Interactive arrow-key mode selection during initialization
- Mode-specific system prompts for different coaching styles
- Custom `/learn` commands tailored to each mode's learning approach
- Mode persistence in `.learning/config.json`
- Exam mode includes specialized practice-creator agent for tests and quizzes

### Changed

- Reorganized template structure into `modes/` directory
- Mode-specific coaching personalities and teaching approaches
- Each mode has unique syllabus generation strategy
- Removed single-purpose templates in favor of mode-specific variants

### Added

- `inquirer` dependency for interactive CLI prompts
- Four complete system prompt variations (one per mode)
- Four custom `/learn` command implementations
- Exam-specific practice-creator agent for test preparation

## [1.0.0] - 2025-11-11

### Features

- Initial release of Learn FASTER CLI tool
- FASTER learning framework implementation
- Spaced repetition review scheduler
- Syllabus generation and progress tracking
- Integration with Claude Code CLI
- Three slash commands: /learn, /review, /progress
- Practice creator agent for hands-on learning
- macOS Reminders integration support
- Socratic method coaching approach

### Documentation

- Comprehensive README with installation and usage instructions
- FASTER framework reference documentation
- Template-based learning system
