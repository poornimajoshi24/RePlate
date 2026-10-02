# CLAUDE.md: rules for Claude Code in this repo

This repo is AnnaSetu, a surplus-food platform built as a **learning project**. The owner is learning backend + AI/ML by building it.
The owner must be able to explain every line in an interview, so:

1. **Small, focused changes.** Only build what the prompt asks for. No extra libraries, features or "future-proofing".
2. **Explain after every change:** list each file created/changed and, in plain simple language, what it does and why it exists.
3. **No black boxes.** Prefer simple, readable code over clever code. Add short comments only where the *why* isn't obvious.
4. **Don't add technologies early.** No DB, auth, Redis, Docker, queues etc. unless the prompt explicitly asks for them.
5. **Never run destructive commands** (deleting files/folders, force-pushing, dropping databases) without asking first.
6. **Tell the owner how to verify** the change manually (exact commands) at the end.

Learning context lives in `docs/journey/` (ROADMAP.md, PROGRESS.md).
