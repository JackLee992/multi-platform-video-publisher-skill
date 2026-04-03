# Repository Context

- Local checkout:
  Use any local clone of the repository.
- GitHub repository:
  `https://github.com/JackLee992/multi-platform-video-publisher`

## Repository Purpose

This repository contains a local-first video publishing toolchain for:

- Xiaohongshu
- Douyin
- WeChat Channels

It includes:

- draft creation and persistence
- title, description, and cover suggestion generation
- a local FastAPI review interface
- browser session reuse helpers
- platform publisher runners
- tests for the publish workflow primitives

## Important Boundaries

- Runtime drafts, copied browser profiles, videos, and generated media are intentionally excluded from version control.
- The repository is designed for local operator-assisted publishing, not unattended cloud automation.
- Platform UI structures can drift; verify selectors and post-submit states on real pages when behavior changes.

