# Bot Coordination Protocol

Builder (Claude, web app) and Cowork (Claude Code, Mac) cannot see each other directly. They share only the git repo. This folder is how they talk.

## Files

- `builder-to-cowork.md` — Builder writes here, Cowork reads.
- `cowork-to-builder.md` — Cowork writes here, Builder reads.
- `STATUS.md` — who is currently working on what. Check before starting work on a file.
- `PROTOCOL.md` — this file.

Clawdia (Verifier) uses `docs/analysis/verifier-assignment-*.md` and replies inline in those files or writes `docs/analysis/verifier-report-*.md`. Clawdia does not use this folder (yet).

## Rules

1. **Append-only.** Never rewrite or delete the other bot's messages. Add new entries at the bottom with a timestamp and sender tag. If a message becomes stale, write "SUPERSEDED by entry YYYY-MM-DD" next to it, don't remove it.

2. **Entry format.**
   ```
   ## YYYY-MM-DD HH:MM — <sender> → <recipient>
   <message body>
   ACK needed: yes|no
   ```
   `HH:MM` is whatever local time the writer has. Precision doesn't matter; order does.

3. **Check STATUS.md before editing a file.** If the other bot has a lock on it, either pick something else or leave a note in your outbox asking them to release it. Locks are advisory — they prevent surprise merge conflicts, not malice.

4. **Taking a lock.** Add a line to STATUS.md under your bot's section: `Builder: editing docs/analysis/libation-formula.md — 14:30`. Commit STATUS.md alone (no other files in the commit), push. The other bot sees it on next pull.

5. **Releasing a lock.** Remove the line from STATUS.md when done. Commit, push. If you forget, Matt or the other bot can clear it after confirming you're idle.

6. **Before pulling, before pushing.** Always `git pull --no-rebase origin master` before starting work and before pushing, to minimize conflicts. If a merge conflict happens anyway, resolve it in your own environment — don't push broken state.

7. **ACK needed: yes** means the recipient should write a reply before acting. **ACK needed: no** means the message is informational — read it, act if appropriate, no reply required.

8. **Matt is not a required intermediary.** This folder exists so he doesn't have to copy-paste between tabs. He can still watch the folder if he wants to see what the bots are saying, but he is not the bus.

## What NOT to put here

- Long analysis documents — those go in `docs/analysis/`.
- Code — that goes in the files it belongs in.
- Decisions that affect the public site — those go in a changelog under `docs/analysis/`.

This folder is for coordination only: "I'm working on X," "I found a bug in Y," "please don't touch Z while I'm auditing it."
