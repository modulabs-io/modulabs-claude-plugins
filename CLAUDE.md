# CLAUDE.md

This file provides guidance to Claude Code when working with this repository.

## Project Overview

This is a **registry-only** marketplace for Claude Code plugins. This repository contains:
- A catalog of plugins hosted in external repositories
- Documentation for plugin submission
- Validation schemas

**Important**: This repo does NOT contain plugin code. Plugins live in their own GitHub repositories and are referenced here via `.claude-plugin/marketplace.json`.

## Repository Structure

```
modulabs-claude-plugins/
├── .claude/
│   ├── settings.json           # Claude Code project settings
│   └── skills/
│       └── add-plugin/
│           └── SKILL.md        # Skill for adding plugins to registry
├── .claude-plugin/
│   └── marketplace.json        # THE REGISTRY - references external plugin repos
├── schemas/
│   └── marketplace.schema.json # JSON schema for validation
├── docs/
│   ├── PLUGIN_REQUIREMENTS.md  # Requirements for plugins to be listed
│   └── SUBMITTING.md           # How to submit a plugin
├── CLAUDE.md                   # This file
├── README.md                   # Main documentation
└── LICENSE                     # MIT license
```

## Development Workflow

This project uses **trunk-based development**:
- Work directly on `main` branch for documentation/schema changes
- Plugin additions should come via Pull Requests
- No long-lived feature branches

## Key Files

### `.claude-plugin/marketplace.json`

The core registry file. Contains an array of plugin entries that reference external repositories:

```json
{
  "plugins": [
    {
      "name": "plugin-name",
      "source": {
        "source": "github",
        "repo": "owner/repo-name",
        "ref": "v1.0.0"
      },
      "description": "What the plugin does",
      "version": "1.0.0"
    }
  ]
}
```

### Adding a Plugin to the Registry

1. Verify the plugin meets requirements in `docs/PLUGIN_REQUIREMENTS.md`
2. Add an entry to `.claude-plugin/marketplace.json`
3. Validate the JSON against `schemas/marketplace.schema.json`
4. Submit a PR with the plugin author's information

## Validation Requirements

When reviewing plugin submissions:
- Plugin repository must exist and be accessible
- `plugin.json` in the plugin repo must have required fields
- Version in registry must match a valid tag/ref in the plugin repo
- Plugin must have a README with usage documentation
- License must be MIT or compatible

## Naming Conventions

- Plugin names use **kebab-case** (e.g., `my-awesome-plugin`)
- All plugins must use **semantic versioning** (e.g., `1.0.0`)

## Commands

No build commands - this is a documentation/registry repository.

Validate marketplace.json:
```bash
# Check JSON syntax
python -m json.tool .claude-plugin/marketplace.json > /dev/null && echo "Valid JSON"
```

## Skills

### `/add-plugin`

Adds a new plugin to the marketplace by fetching metadata from its GitHub repository.

**Usage:**
```
/add-plugin <owner/repo>
/add-plugin https://github.com/owner/repo
```

**Example:**
```
/add-plugin anthropics/claude-test-plugin
```

**What it does:**
1. Fetches `plugin.json` from the GitHub repository
2. Gets the latest release tag
3. Validates README.md and LICENSE exist
4. Checks for duplicate plugin names
5. Adds entry to `.claude-plugin/marketplace.json`
6. Validates the JSON syntax
7. Auto-commits with `feat: add plugin <name>`

**Requirements for the plugin repository:**
- Must have `plugin.json` with required fields (name, version, description, author, type, license)
- Must have at least one tagged release
- Must have README.md
- Must have LICENSE file

See `docs/PLUGIN_REQUIREMENTS.md` for full plugin requirements.

## Commit Conventions

This project uses **conventional commits** for automated semantic versioning.

### Format

```
<type>(<scope>): <description>
```

### Types

| Type | Description | Version Bump |
|------|-------------|--------------|
| `feat` | New feature | MINOR (1.x.0) |
| `fix` | Bug fix | PATCH (1.0.x) |
| `docs` | Documentation only | No release |
| `style` | Formatting, no code change | No release |
| `refactor` | Code change, no feature/fix | No release |
| `perf` | Performance improvement | No release |
| `test` | Adding/updating tests | No release |
| `chore` | Maintenance tasks | No release |
| `ci` | CI/CD changes | No release |

### Breaking Changes

Add `!` after type or include `BREAKING CHANGE:` in the footer:
```
feat!: remove deprecated API
```

This triggers a MAJOR version bump (x.0.0).

### Examples

```bash
feat: add new plugin validation endpoint
fix: correct JSON schema validation
docs: update submission guidelines
chore: update dependencies
feat(registry): add plugin search functionality
feat!: change plugin manifest format
```
