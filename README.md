# claude-mods

A Claude Code **plugin marketplace** serving my mods, each hosted in its own
repository. The marketplace is the catalog; the mods are the code.

| Plugin | Source repo | What it does |
|---|---|---|
| `collapse-tools` (Claude Fold) | [jlopez/claude-mod-collapse-tools](https://github.com/jlopez/claude-mod-collapse-tools) | Collapses each tool call in the transcript to one clickable line, in a color you pick, showing the model's own description of the call where it has one |

`collapse-tools` is a fork of
[0xnicholasy/claude-mod-collapse-tools](https://github.com/0xnicholasy/claude-mod-collapse-tools)
(MIT). The fork exists so the mod can evolve past upstream at my pace; the
upstream remote stays wired so fixes flow in either direction.

## Install

```bash
claude plugin marketplace add jlopez/claude-mods
claude plugin install collapse-tools@claude-mods
```

Then start a new Claude Code session: plugins load at startup.

The marketplace shares its name (`claude-mods`) with 0xnicholasy's. Only one
marketplace of a given name can be registered at a time, so switching from
upstream means removing theirs first:

```bash
claude plugin uninstall collapse-tools@claude-mods
claude plugin marketplace remove claude-mods
claude plugin marketplace add jlopez/claude-mods
claude plugin install collapse-tools@claude-mods
```

## How plugins are served

Each entry in [`.claude-plugin/marketplace.json`](.claude-plugin/marketplace.json)
is a `git-subdir` source: the plugin's repo URL plus the path of the plugin
folder inside it (`.claude/skills/<name>`). Claude Code clones the repo at
install time and caches the subdirectory under
`~/.claude/plugins/cache/claude-mods/<plugin>/<version>/`.

Two consequences:

- **Changes ship through the plugin repo**, not this one. Edit the mod in its
  repo, bump `version` in its `plugin.json`, then mirror the bump in the entry
  here. `claude plugin update collapse-tools` pulls the new version.
- **To iterate without the cache**, load the plugin folder directly:
  `claude --plugin-dir <plugin-repo>/.claude/skills/collapse-tools`.

## Validate

```bash
claude plugin validate .
```
