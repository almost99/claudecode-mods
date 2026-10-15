# cache-tax

- **Verdict:** Approved with notes
- **Reviewed:** 2026-10-15
- **Source:** https://github.com/karanb192/cache-tax
- **Commit:** `06cac47ec125a41a4aeeb78a6b006bec8cc6d6ed` (2026-10-04)
- **Author(s):** Karan Bansal, sole author. The repo started 2026-09-18 and is version 2.2.1.
- **Install path checked:** The author's own install command uses the `karanb192/claude-code-mods` marketplace. That marketplace's `cache-tax` entry points straight at this repo's default branch, unpinned. This marketplace pins it instead.

## What it does

- Tracks whether the one-hour prompt cache is "warm" or "cold," and shows that state in a band above the prompt.
- **Guard:** if you return after more than an hour to a large conversation (50,000+ tokens), it blocks your first message once and shows the estimated cost of re-sending the whole conversation. Send it again to go through.
- **Keep-warm (`/keepwarm`):** while you're away, it sends a tiny ping about every 50 minutes so the cache stays cheap to read.
- Commands: `/keepwarm [6h | 90m | always | off | status]` and `/cache-tax [status | guard warn | guard refuse]`.

## What it can't do

- No internet calls to any outside server, including the author's website.
- No shell commands.
- No reading or writing files.
- Reads one environment variable, `NO_COLOR`, a display preference.
- The icons are images embedded in the code (checked: real PNG and SVG data). Nothing is downloaded at runtime.

## What it sees and keeps

- **Your prompts:** it checks only whether each starts with `/`. The text is not stored, logged, or changed.
- **Token counts and model name:** from data Claude Code already tracks.
- **Saved in its own local storage:** the keep-warm deadline and ping period (per session), the guard mode, and the "always" switch. Nothing else.

## What leaves your machine

- **The keep-warm ping** is a real model request to Anthropic: "Reply with the single word: warm." It goes through Claude Code's normal connection and carries your conversation like any other message. It does not go to a third party.
- **It costs tokens.** On a Claude Team plan that means usage against your limits. The author notes that how cache reads count toward plan limits isn't documented.

## Things to know before installing

- **It may block one message** when you come back to a big, cold conversation. To get a warning instead, run `/cache-tax guard warn`.
- **It turns itself on.** After you pay for a cold re-send, it arms keep-warm for 3 hours on its own. Run `/keepwarm off` to stop it.
- Requires Claude Code 2.1.287 or later. Organization policy can block mods.

## Risks

- **Low.** The code is small, readable, and does what the README says.
- Main exposure was unreviewed future updates from a single author. Pinning removes that.

## Files read

- `hooks/register.ts` (520 lines): the only module Claude Code runs. Read in full.
- `hooks/status-icons.ts` (31 lines): embedded icon data. Read in full; contents checked.
- `hooks/hooks.json`, `.claude-plugin/plugin.json`: read in full.
- Not loaded by Claude Code, so only skimmed: `site/`, `docs/`, `tests/`, `tools/`, `.github/`.
