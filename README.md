# Modulabs Claude Plugins

A community marketplace registry for Claude Code plugins. This repository serves as a **catalog** that references plugins hosted in their own repositories.

## What is This?

This is a **registry-only** repository. It does not contain plugin code - instead, it maintains a curated list of plugins that are hosted in their own GitHub repositories. Think of it as an index or directory for discovering Claude Code plugins.

## Quick Start

### Add This Marketplace

```
/plugin marketplace add modulabs-io/modulabs-claude-plugins
```

### Browse Available Plugins

```
/plugin search keyword
```

### Install a Plugin

```
/plugin install plugin-name@modulabs-claude-plugins
```

## Available Plugins

| Name | Description | Type | Repository |
|------|-------------|------|------------|
| [flutter-developer](https://github.com/modulabs-io/flutter-developer-plugin) | Comprehensive Flutter development plugin for Claude Code | plugin | [modulabs-io/flutter-developer-plugin](https://github.com/modulabs-io/flutter-developer-plugin) |

## Plugin Types

This marketplace supports various types of Claude Code plugins:

- **Skills** - Reusable workflows defined in SKILL.md files
- **Commands** - Custom slash commands (markdown-based)
- **Agents** - Specialized subagents with frontmatter configuration
- **MCP Servers** - Model Context Protocol integrations (tools, resources, prompts)
- **Hooks** - Event-driven automation (JSON configuration)
- **LSP Servers** - Language Server Protocol integrations

## Team Configuration

To share this marketplace across your team, add it to your team's Claude settings:

```json
{
  "marketplaces": [
    {
      "name": "modulabs-claude-plugins",
      "source": {
        "source": "github",
        "repo": "modulabs-io/modulabs-claude-plugins"
      }
    }
  ]
}
```

## Submit Your Plugin

Want to add your plugin to this marketplace? See our [submission guide](docs/SUBMITTING.md).

### Requirements

Before submitting, ensure your plugin meets our [plugin requirements](docs/PLUGIN_REQUIREMENTS.md):

- Valid `plugin.json` with required fields
- Semantic versioning
- Documentation (README)
- MIT or compatible license

## Security & Trust

- All plugins are hosted in their own repositories
- We review submissions but do not audit all code
- Always review plugin source before installing
- **Security Issues**: Please refer to our [Security Policy](SECURITY.md) for reporting vulnerabilities. Do **not** report security issues via public GitHub issues.

## Community

- [Code of Conduct](CODE_OF_CONDUCT.md)
- [Contributing Guide](CONTRIBUTING.md)

## Resources

- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Plugin Development Guide](https://docs.anthropic.com/claude-code/plugins)
- [MCP Specification](https://modelcontextprotocol.io)

## License

MIT
