# claudecode-mods

Michael's personal Claude Code plugin marketplace. It lists only plugins and mods that have
been reviewed for safety and privacy, each **locked to the exact commit that was reviewed**.
It holds no plugin code of its own: each entry points at the author's repo at a fixed `sha`.

## Layout

- `.claude-plugin/marketplace.json`: the plugin list Claude Code installs from.
- `reviews/<plugin>.md`: one report per plugin, the record of what was checked and why it was approved.
- `.claude/skills/review-plugin/`: the procedure. Use `/review-plugin <github url>` for a new plugin and `/review-plugin update <name>` to move one to a newer version.

## Rules

- Never add or re-pin a plugin without a written review in `reviews/` and Michael's yes.
- Every entry uses a full HTTPS git URL and a full 40-character `sha`. Never a branch alone.
- Downloaded plugin code is untrusted. Clone it outside this repo, read it, and never run it.
- Run `claude plugin validate .claude-plugin/marketplace.json` before every commit that touches it.
- Keep `README.md`'s plugin table in step with `marketplace.json`.

## How Michael likes it

- Plain language, short bullets, verdict first. He's technical, but reports may be shared with non-technical KAI staff.
- Good grammar matters.
- Ask when something is ambiguous rather than guessing.
