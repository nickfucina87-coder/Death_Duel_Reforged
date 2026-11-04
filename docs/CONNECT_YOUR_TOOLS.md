# Use the same repository in ChatGPT, Cursor, and Claude

Repository: https://github.com/nickfucina87-coder/Death_Duel_Reforged

GitHub is the shared record. Connecting a tool does not merge private chats, subscriptions, or model memory.

## Connection status

| Tool | Prepared or verified here | Still needed on your device |
| --- | --- | --- |
| ChatGPT in this conversation | GitHub read/write access verified; repository cloned in this session | No additional authorization needed for the already verified repository actions here |
| Cursor | Shared AGENTS.md plus an always-applied project rule committed | Open or clone this repository in Cursor; verify your GitHub authentication before pushing |
| Claude Code | CLAUDE.md imports shared instructions and current status | Open a terminal in this repository and start your installed Claude Code; complete its sign-in/trust flow if required |
| Claude website/app | Public repository URL and shared documents are available | Select this repository through the GitHub integration if available on your account, or supply the shared documents as project context |

Cursor and Claude account connections have not been verified from this session. Repository instruction files prepare context; they do not grant account access.

## Cursor on your PC

If this repository is already open in Cursor, fetch/pull the latest changes and start a new agent conversation. Do not create a second copy unnecessarily.

Otherwise, use Git: Clone from Cursor's command palette and paste:

```text
https://github.com/nickfucina87-coder/Death_Duel_Reforged.git
```

Open the cloned folder. If pushing requires authentication, complete Cursor/Git's normal GitHub sign-in flow.

## Claude Code on the same PC

Use the same local folder Cursor opened. In that folder's terminal, start your installed CLI:

```text
claude
```

CLAUDE.md points Claude Code to AGENTS.md and docs/STATUS.md. Use /memory to inspect loaded project instructions. Complete any normal sign-in or repository-trust step yourself; never paste credentials into a project document.

For Claude on the website/app, connection controls and availability depend on your account. Connect GitHub there if offered, select this repository, and explicitly ask Claude to read the shared instructions. A public URL alone does not establish a persistent connection.

## Starter instruction for any tool

> Work with nickfucina87-coder/Death_Duel_Reforged. Read AGENTS.md, README.md, and docs/STATUS.md first. This task is GitHub setup and documentation only. Do not build game code or select an engine. Report the branch and latest commit you inspected before making changes.

## Keep all three aligned

1. Fetch/pull before editing. If there are local changes, preserve them and resolve the situation before pulling.
2. Work on a separate branch when multiple agents are editing.
3. Commit decisions and progress to the repository; update docs/STATUS.md after substantive work.
4. Push changes so the other tools can fetch them.
5. Do not force-push over another person's work.

## Official references

- Cursor project rules: https://cursor.com/docs/rules
- Claude Code project memory: https://code.claude.com/docs/en/memory

These explain the instruction-file mechanisms. Actual application sign-in and repository access must be verified separately.
