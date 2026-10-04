For your Electrope project, I'd use three layers of persistence so Claude Code can survive terminal closures, Windows restarts, context compaction, and even starting an entirely new conversation without losing track of what it's building.

The important distinction is that Claude's conversation history, its project instructions, and the actual project files are three separate things.

Also, when starting Claude Code, make sure you're inside the project directory—not `C:\Users\aardizzone`, as happened after your previous reboot.

## 1. Resume the same Claude session after reboot

In Windows PowerShell:

```
cd "$HOME\Projects\approval-platform"

# Resume the most recent session for THIS project
claude --continue
```

Or, if you want to choose a particular previous session:

```
cd "$HOME\Projects\approval-platform"

claude --resume
```

The second command opens the session selector.

Inside Claude Code, you can also use:

| Command                         | Purpose                                              |
| ------------------------------- | ---------------------------------------------------- |
| `/rename electrope-development` | Give the current session a recognizable name         |
| `/resume`                       | Browse and resume previous sessions                  |
| `/context`                      | Inspect context-window usage                         |
| `/compact`                      | Summarize conversation history to free context       |
| `/memory`                       | Inspect persistent instructions and automatic memory |

Claude Code saves conversations locally under `~/.claude/projects/`. Resuming reopens the existing conversation rather than creating an unrelated one.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://code.claude.com\&sz=32)

Claude Code Docs

+1



## 2. Make Claude retain the project's development state permanently

This is the improvement I'd prioritize.

Your repository already has `CLAUDE.md`, but that file primarily establishes instructions and architectural conventions.

I'd introduce another file:

`docs/PROJECT_STATE.md`

That file becomes the project's living development journal—not a transcript, but a concise record of where everything stands.

The ideal structure:

approval-platform/

`CLAUDE.md`

Permanent rules

`docs/`

`PROJECT_STATE.md`

Current progress

`ROADMAP.md`

Next milestones

`deployment.md`

Infrastructure

Then add this line to the existing `CLAUDE.md`:

```
## Current Development Context

Always load the current project state:
@docs/PROJECT_STATE.md
```

Claude Code supports importing additional Markdown files using the `@path` notation. These are loaded alongside `CLAUDE.md` when starting a session.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://code.claude.com\&sz=32)

Claude Code Docs

+1



Keep the imported state file concise so it doesn't unnecessarily consume context.

## 3. Give Claude this instruction once

This is the part I'd implement immediately, before handing it the substantial Service Catalog development specification.

# Establish persistent development continuity

Before starting our next milestone, improve this repository's Claude Code session persistence.

I want the project to remain understandable and resumable after:

- Windows restarts.
- Claude Code updates.
- Terminal closures.
- Context compaction.
- Beginning entirely new Claude Code sessions.
- Switching models.

Please implement the following:

1. Review our existing CLAUDE.md. Preserve its permanent project instructions.
2. Create docs/PROJECT_STATE.md, documenting:
   - Current architecture and completed modules.
   - Most recently verified deployed revision.
   - Current development branch/commit.
   - Outstanding local changes.
   - Database schema version and migration considerations.
   - Current milestone.
   - What has been completed.
   - Decisions already made.
   - Known bugs and blockers.
   - The next concrete actions.
   - Any explicit outstanding user authorizations.
3. Create docs/ROADMAP.md containing our major planned development milestones, including the Tiered Service Catalog and Entitlement Visual System.
4. Update CLAUDE.md to import docs/PROJECT_STATE.md using the supported @path syntax.
5. Establish a standing development rule:

After each meaningful implementation checkpoint, successful deployment, major architectural decision, or before ending a long work session, update PROJECT_STATE.md to accurately reflect the current state.

Replace outdated information rather than endlessly appending session summaries.

6. On every NEW Claude Code session, read the imported project state, inspect git status and recent commits, and reconcile any discrepancies before continuing development.
7. Never assume a deployment succeeded merely because it was planned or committed. Distinguish local implementation, pushed commits, passing CI, and verified staging deployments.
8. Never store credentials, invitation tokens, private keys, or other secrets in these documentation files.

The objective is for me to open a fresh PowerShell terminal tomorrow, run Claude from the approval-platform repository, and say "continue development" without having to manually reconstruct the previous day's work.

Implement this now and commit the documentation changes using my personal repository Git identity.

Do not deploy or modify infrastructure solely for this documentation task.

## 4. My recommended daily workflow

Once you've established this, your routine becomes extremely simple.

When starting development:

```
cd "$HOME\Projects\approval-platform"
claude --continue
```

Before deliberately ending a long session, tell Claude:

> Update PROJECT_STATE.md with everything important accomplished today, reconcile it against Git, and record exactly where development should resume.

Then, if its context window is getting crowded, use:

```
/compact Preserve the active milestone, pending implementation decisions, blockers, and deployment state.
```

The conversation is still resumable afterward. However, because compaction summarizes earlier context, your persistent project files should carry the details you cannot afford to lose.&#x20;

[image](https://www.google.com/s2/favicons?domain=https://code.claude.com\&sz=32)

Claude Code Docs

+1



The outcome I want: instead of Claude relying on remembering a 30,000-token conversation, it starts each new session with a compact, authoritative understanding of Electrope—what exists, what is deployed, what you're currently building, and what it should do next.
