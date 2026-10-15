# savvy-progress

- **Verdict:** Approved with notes
- **Reviewed:** 2026-10-15
- **Source:** https://github.com/JohnnyVizz/claude-kit (folder `plugins/savvy-progress`)
- **Commit:** `c871c153ead54ad9547cc717d0f3e5a676c73986` (2026-10-13)
- **Author(s):** JohnnyVizz, with about 10 outside contributors via pull requests. The repo started 2026-10-04 and the plugin is version 1.2.1.
- **Install path checked:** The author's `claude-kit` marketplace lists this plugin from its own folder. This marketplace pulls only that folder, at the pinned commit.

## What it does

- Draws a progress bar above the prompt during the author's **savvy-flow** skill. That skill is not reviewed or listed here.
- Adds an **Agents** panel, opened with `/agents-info`. It shows each subagent Claude runs, with its model, context used, estimated cost, and time.
- Without savvy-flow, the panel still works for any subagents. It opens on its own only for savvy agents, unless you set `autoOpen` to `any`.
- Optional settings: panel language (auto, en, ru, he) and auto-open behavior.

## What it can't do

- No internet calls, no shell commands, and no reading or writing files.
- **No model requests of its own**, so it adds no extra cost of that kind.
- Saves nothing. Its data lives in memory and is gone when Claude Code closes.
- Reads only language info: Claude Code's `language` setting, then the `LC_ALL`, `LC_MESSAGES`, and `LANG` environment variables.

## What it sees and keeps (in memory only)

- Each subagent's type, short description, model, effort, token counts, and timing.
- The plan and progress counts that savvy-flow reports to it.
- Subagent descriptions are escaped before they're drawn, so text in them can't break the panel.

## What leaves your machine

- Nothing beyond what Claude Code already sends.

## Things to know before installing

- **It adds two tools Claude can call.**
  - `progress`: used by savvy-flow in the main session.
  - `step`: placed in every subagent's tool list, which adds a little to each subagent request.
  - Both only update the drawing.
- **It adds this text to the end of "savvy-" subagents' instructions** (exact wording):
  > Progress reporting: before any other work, call `mcp__savvy-progress__step` with `total` (your plan in 3-8 steps) and `done: 0`; call it again with `done` and a few-word `note` as each step finishes. It only draws a progress bar.

  Other subagents are left untouched.
- **It watches Agent tool calls** for savvy- agents, only to count them. It always passes them through unchanged.

## Risks

- **Low.** It's display-only, with a small capability footprint.
- Main exposure was unreviewed future changes from a busy multi-contributor repo. Pinning removes that.

## Files read

- `hooks/register.tsx` (1,271 lines): the only module Claude Code runs. Read in full.
- `hooks/hooks.json`, `.claude-plugin/plugin.json`, `types/index.d.ts`: read in full.
- Not loaded by Claude Code, so not reviewed: `hooks/*.test.ts(x)`, `README.md`, and the repo's other plugins (`savvy-flow`, `session-band`).
