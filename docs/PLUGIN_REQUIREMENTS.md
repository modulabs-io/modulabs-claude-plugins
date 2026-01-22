# Plugin Requirements

Requirements for plugins to be listed in the Claude Plugin Marketplace.

## Required Files

Your plugin repository must include:

### 1. `plugin.json`

A manifest file with the following required fields:

```json
{
  "name": "your-plugin-name",
  "version": "1.0.0",
  "description": "What your plugin does",
  "author": {
    "name": "Your Name"
  },
  "type": "skill|command|agent|mcp-server|hook|lsp-server",
  "license": "MIT"
}
```

### 2. `README.md`

Documentation that includes:
- What the plugin does
- Installation instructions
- Usage examples
- Configuration options (if any)
- License information

### 3. License File

A `LICENSE` file with MIT or a compatible open-source license.

## Plugin Structure by Type

### Skills

```
your-skill-plugin/
├── plugin.json
├── README.md
├── LICENSE
└── SKILL.md          # The skill definition
```

### Commands

```
your-command-plugin/
├── plugin.json
├── README.md
├── LICENSE
└── commands/
    └── your-command.md
```

### Agents

```
your-agent-plugin/
├── plugin.json
├── README.md
├── LICENSE
└── agents/
    └── your-agent.md  # With YAML frontmatter
```

### MCP Servers

```
your-mcp-plugin/
├── plugin.json
├── README.md
├── LICENSE
├── src/
│   └── index.ts      # Server implementation
└── package.json
```

### Hooks

```
your-hook-plugin/
├── plugin.json
├── README.md
├── LICENSE
└── hooks.json        # Hook configuration
```

## Naming Conventions

- Plugin names must use **kebab-case** (e.g., `my-awesome-plugin`)
- Names should be descriptive and unique
- Avoid generic names like `plugin` or `tool`

## Versioning

- Use **semantic versioning** (MAJOR.MINOR.PATCH)
- Tag releases in your repository (e.g., `v1.0.0`)
- The version in `plugin.json` must match the git tag

## Security Guidelines

Your plugin must NOT:
- Request unnecessary permissions
- Execute arbitrary code from external sources
- Store sensitive data insecurely
- Make network requests without user awareness
- Modify files outside its intended scope

## Quality Standards

- Code should be well-documented
- Include error handling
- Provide meaningful error messages
- Test your plugin before submission
- Keep dependencies minimal and up-to-date

## Compatibility

- Specify minimum Claude Code version if required
- Document any system requirements
- Test on multiple platforms if applicable
