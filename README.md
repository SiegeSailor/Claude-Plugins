# Claude-Plugins

Personal [Claude Code](https://claude.com/claude-code) plugins, published as a marketplace.

## Install

```shell
/plugin marketplace add SiegeSailor/Claude-Plugins
/plugin install conventional-commit@siegesailor
```

Adding the marketplace makes every plugin below available; installing one enables its skills in the session.

## Plugins

| Plugin                                                       | Provides                                                                         |
| ------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| [`conventional-commit`](./plugins/conventional-commit/)      | One-line Conventional Commits messages, with the type-to-release table and scopes read from the host repository |

## Layout

```text
.claude-plugin/marketplace.json     the marketplace, listing every plugin below
plugins/<name>/
  .claude-plugin/plugin.json        the plugin's own manifest
  skills/<name>/SKILL.md            the skill Claude loads
```

A plugin is listed in `marketplace.json` by a relative `source` path, so the marketplace and the plugins it serves live in this one repository.

## Adding a Plugin

1. Create `plugins/<name>/.claude-plugin/plugin.json` with `name`, `version`, and `description`.
2. Add its skills under `plugins/<name>/skills/<skill>/SKILL.md`, each with `name` and `description` front matter — the description states **when** to use the skill, not what it does.
3. Add an entry to `.claude-plugin/marketplace.json` with `"source": "./plugins/<name>"`.
4. Record it in the table above.

## License

[MIT](./LICENSE.md)
