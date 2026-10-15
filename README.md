# claudecode-mods

Claude Code plugins and mods I've reviewed for safety and privacy. Each one is locked to the
exact version that was reviewed, so the author's later changes can't reach my machine
until they're reviewed too.

## Install

```
claude plugin marketplace add https://github.com/almost99/claudecode-mods.git
claude plugin install <plugin-name>@claudecode-mods
```

Restart Claude Code, or run `/reload-plugins` in an open session.

## Plugins

| Plugin | What it does | Locked to | Review |
|---|---|---|---|
| cache-tax | Keeps the prompt cache warm during breaks and stops a costly "cold" send once. Pings cost tokens. | `06cac47` | [Report](reviews/cache-tax.md) |
| savvy-progress | Progress bar above the prompt plus an Agents panel showing subagents' model, cost and time. | `c871c15` | [Report](reviews/savvy-progress.md) |

## Updating

When a plugin's author releases changes, nothing updates on its own. Open this repo in Claude
Code and run `/review-plugin update <name>`. It reviews only what changed, and moves the lock
forward if I approve. Then run:

```
claude plugin marketplace update claudecode-mods
claude plugin update <plugin-name>@claudecode-mods
```

## Adding a plugin

Open this repo in Claude Code and run `/review-plugin <github url>`.
