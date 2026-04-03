---
name: multi-platform-video-publisher
description: Use when a user wants to prepare, review, or publish one video across Xiaohongshu, Douyin, and WeChat Channels from a local-first workflow, especially when Chrome session reuse, cover selection, title validation, or per-platform browser automation is involved.
---

# Multi-Platform Video Publisher

## Overview

Use this skill when the task is to run or extend the local multi-platform video publishing workflow backed by the `multi-platform-video-publisher` repository.

Read [references/repo-context.md](references/repo-context.md) first to locate the local checkout and GitHub repository.

## Quick Start

Clone or open the project repository, then work from the repository root:

```bash
git clone https://github.com/JackLee992/multi-platform-video-publisher.git
cd multi-platform-video-publisher
```

Create or refresh the virtual environment, then install dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -e .[dev]
```

Run the full test suite before claiming the workflow is healthy:

```bash
./.venv/bin/python -m pytest -q
```

## Main Workflow

1. Create a publish draft from a local video path.
2. Generate transcript-driven title, description, and cover suggestions.
3. Open the local review UI and require final human approval.
4. Reuse the current Chrome session when possible.
5. Fall back to Playwright only when browser reuse is blocked.
6. Execute platform-specific publish steps and verify each platform's post-submit state.

## Commands

- Create a real draft:

```bash
./.venv/bin/python -m mvpublisher.cli create-draft /absolute/path/to/video.mov
```

- Start the review app:

```bash
./.venv/bin/python -m mvpublisher.cli serve-review
```

- Publish an approved draft:

```bash
./.venv/bin/python -m mvpublisher.cli publish-draft <draft-id>
```

## Execution Rules

- Prefer the current logged-in Chrome session before opening a separate browser.
- Keep final approval human-confirmed before calling any publish flow.
- Never commit or upload `runtime/`, copied browser profiles, local videos, generated covers, or publish artifacts.
- Treat platform success as verified only after checking the resulting page state.
- Respect per-platform validation rules. For example, WeChat Channels short titles must stay within 16 Chinese characters.

## Key Files

- CLI entry: `src/mvpublisher/cli.py`
- Draft workflow: `src/mvpublisher/workflows.py`
- Review app: `src/mvpublisher/web/app.py`
- Platform publishers: `src/mvpublisher/publishers/`

## Validation

Representative checks:

```bash
./.venv/bin/python -m pytest -q
./.venv/bin/python -m mvpublisher.cli --help
./.venv/bin/python -m mvpublisher.cli serve-review --help
```

For real publishing validation, use a non-sensitive local video, confirm the draft in the review UI, and then verify each platform's result page after submission.
