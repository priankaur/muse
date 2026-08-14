# MUSE Worktree Setup

## Preferred Codex branch/worktree

Use:

`codex/muse-static-experience`

If creating the worktree manually from the repository root:

```bash
git fetch origin
git switch <default-branch>
git pull --ff-only
git worktree add ../muse-static-experience -b codex/muse-static-experience
cd ../muse-static-experience
```

If the branch already exists remotely:

```bash
git fetch origin
git worktree add ../muse-static-experience codex/muse-static-experience
```

In the Codex desktop app, its built-in worktree support can isolate the task automatically; use the same branch intent and ensure the agent reads `AGENTS.md` before implementation.

## First worktree task

Do not build every screen immediately.

Start with:

1. repository/project scaffold,
2. fixed 4:3 stage,
3. tokens/background/HUD,
4. blank window-frame component,
5. hardware strip,
6. component gallery,
7. first approved screens.

Only after the visual foundation is accepted should the rest of the screen inventory be implemented.
