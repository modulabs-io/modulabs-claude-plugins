# Submitting a Plugin

Guide for submitting your plugin to the Claude Plugin Marketplace.

## Prerequisites

Before submitting, ensure your plugin:

1. Meets all [plugin requirements](PLUGIN_REQUIREMENTS.md)
2. Has a public GitHub repository
3. Has at least one tagged release
4. Includes proper documentation

## Submission Process

### Step 1: Fork This Repository

Fork the [modulabs-claude-plugins](https://github.com/modulabs-io/modulabs-claude-plugins) repository to your GitHub account.

### Step 2: Add Your Plugin Entry

Edit `.claude-plugin/marketplace.json` and add your plugin to the `plugins` array:

```json
{
  "name": "your-plugin-name",
  "source": {
    "source": "github",
    "repo": "your-username/your-plugin-repo",
    "ref": "v1.0.0"
  },
  "description": "A brief description of what your plugin does",
  "version": "1.0.0",
  "author": {
    "name": "Your Name",
    "email": "your@email.com"
  },
  "keywords": ["category", "relevant", "tags"],
  "license": "MIT",
  "type": "skill"
}
```

### Step 3: Validate Your Entry

Ensure your JSON is valid:

```bash
python -m json.tool .claude-plugin/marketplace.json > /dev/null && echo "Valid JSON"
```

### Step 4: Submit a Pull Request

Create a pull request with:

**Title**: `Add plugin: your-plugin-name`

**Description**:
```markdown
## Plugin Submission

**Plugin Name**: your-plugin-name
**Repository**: https://github.com/your-username/your-plugin-repo
**Type**: skill/command/agent/mcp-server/hook/lsp-server

### Description
Brief description of what your plugin does.

### Checklist
- [ ] Plugin has a valid plugin.json
- [ ] Plugin has a README with documentation
- [ ] Plugin has a LICENSE file
- [ ] Plugin uses semantic versioning
- [ ] I have tested the plugin
```

## Review Process

1. **Automated Checks**: JSON validation and schema compliance
2. **Manual Review**: We verify the plugin repository exists and meets requirements
3. **Approval**: Once approved, your plugin will be merged and available in the marketplace

## Updating Your Plugin

To update a listed plugin:

1. Release a new version in your plugin repository
2. Submit a PR updating the `version` and `ref` in marketplace.json

## Removing a Plugin

To remove your plugin from the marketplace:

1. Submit a PR removing your entry from marketplace.json
2. Include a brief explanation in the PR description

## Questions?

- Open an issue for questions about the submission process
- Check existing plugins for examples
- Review the [plugin requirements](PLUGIN_REQUIREMENTS.md) for detailed specifications
