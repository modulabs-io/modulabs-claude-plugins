# Contributing to Modulabs Claude Plugins

Thank you for your interest in contributing to the Modulabs Claude Plugin Marketplace! This document provides guidelines for contributing to this project.

## Code of Conduct

This project adheres to the [Contributor Covenant Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code. Please report unacceptable behavior to the project maintainers.

## How to Contribute

### Submitting a Plugin

The primary way to contribute is by submitting your Claude Code plugin to the marketplace.

**Quick Steps:**
1. Ensure your plugin meets the [plugin requirements](docs/PLUGIN_REQUIREMENTS.md)
2. Follow the detailed [submission guide](docs/SUBMITTING.md)
3. Submit a pull request with your plugin entry

**Requirements Summary:**
- Public GitHub repository with at least one tagged release
- Valid `plugin.json` manifest
- README.md with documentation
- MIT or compatible license

### Reporting Bugs

Found a bug in the registry or documentation? Please open an issue:

1. Use the [bug report template](.github/ISSUE_TEMPLATE/bug_report.md)
2. Search existing issues first to avoid duplicates
3. Include as much detail as possible:
   - Steps to reproduce
   - Expected vs actual behavior
   - Environment details

**Note:** For bugs in individual plugins, please report them to the plugin's own repository.

### Suggesting Features

Have an idea to improve the marketplace?

1. Use the [feature request template](.github/ISSUE_TEMPLATE/feature_request.md)
2. Clearly describe the problem you're trying to solve
3. Explain your proposed solution
4. Consider alternatives you've thought about

### Improving Documentation

Documentation improvements are always welcome:

- Fix typos or clarify confusing sections
- Add missing information
- Improve examples
- Update outdated content

For small fixes, submit a PR directly. For larger changes, open an issue first to discuss.

## Pull Request Process

### For Plugin Submissions

1. Fork the repository
2. Add your plugin entry to `.claude-plugin/marketplace.json`
3. Validate your JSON: `python -m json.tool .claude-plugin/marketplace.json`
4. Submit a PR using the provided template
5. Wait for review and address any feedback

### For Documentation/Schema Changes

1. Fork the repository
2. Create a descriptive branch (e.g., `docs/clarify-submission-steps`)
3. Make your changes
4. Submit a PR with a clear description

### Commit Messages

This project uses [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <description>
```

**Types:**
- `feat` - New feature (e.g., adding a plugin)
- `fix` - Bug fix
- `docs` - Documentation changes
- `chore` - Maintenance tasks

**Examples:**
```
feat: add plugin awesome-formatter
fix: correct schema validation for MCP servers
docs: clarify plugin versioning requirements
```

### Review Criteria

Pull requests are reviewed for:

1. **JSON Validity** - marketplace.json must be valid
2. **Schema Compliance** - Entries must match the schema
3. **Plugin Accessibility** - Repository must exist and be public
4. **Requirements Met** - Plugin must have required files
5. **Quality** - Documentation should be clear and complete

## Development Setup

This is a registry-only repository with no build process. To work locally:

```bash
# Clone the repository
git clone https://github.com/modulabs-io/modulabs-claude-plugins.git
cd modulabs-claude-plugins

# Validate marketplace.json
python -m json.tool .claude-plugin/marketplace.json > /dev/null && echo "Valid JSON"
```

## Questions?

- **General questions**: Open a discussion or issue
- **Plugin submission help**: See [docs/SUBMITTING.md](docs/SUBMITTING.md)
- **Plugin development**: See [plugin requirements](docs/PLUGIN_REQUIREMENTS.md)
- **Security issues**: See [SECURITY.md](SECURITY.md)

## Recognition

All plugin authors are credited in the marketplace registry. Significant contributors to documentation or tooling may be recognized in the README.

Thank you for contributing!
