---
name: add-plugin
description: Add a new plugin to the marketplace by fetching metadata from its GitHub repository
user-invocable: true
allowed-tools: Read, Edit, Bash, WebFetch, Grep, Glob
argument-hint: "<owner/repo>"
---

# Add Plugin Skill

Add a new plugin to the Claude Plugin Marketplace by fetching metadata from its GitHub repository.

## Input

The `$ARGUMENTS` variable contains the repository reference. Supported formats:
- `owner/repo` (e.g., `anthropics/claude-test-plugin`)
- `https://github.com/owner/repo`

## Workflow

### Step 1: Parse Repository Reference

Extract `owner` and `repo` from `$ARGUMENTS`:
- If full URL: extract from `https://github.com/{owner}/{repo}`
- If short form: split on `/` to get owner and repo
- Remove any trailing `.git` if present

If `$ARGUMENTS` is empty or invalid, show this error:
```
Error: Please provide a repository reference.

Usage: /add-plugin <owner/repo>
Example: /add-plugin anthropics/claude-test-plugin
```

### Step 2: Fetch Plugin Metadata

Use WebFetch to get `plugin.json` from the repository's default branch:

```
URL: https://raw.githubusercontent.com/{owner}/{repo}/HEAD/plugin.json
Prompt: Extract the complete JSON content of this plugin.json file. Return the raw JSON.
```

If plugin.json is not found, show this error:
```
Error: No plugin.json found in {owner}/{repo}

The repository must have a plugin.json file in the root directory.
See: docs/PLUGIN_REQUIREMENTS.md for required fields.
```

Parse the plugin.json and validate these required fields exist:
- `name` (string, kebab-case)
- `version` (string, semver format)
- `description` (string)
- `author` (object with at least `name`)
- `type` (one of: skill, command, agent, mcp-server, hook, lsp-server)
- `license` (string)

If any required field is missing, show:
```
Error: plugin.json is missing required fields: {list of missing fields}

Required fields: name, version, description, author.name, type, license
See: docs/PLUGIN_REQUIREMENTS.md
```

### Step 3: Get Latest Release

Use WebFetch to get the latest release:

```
URL: https://api.github.com/repos/{owner}/{repo}/releases/latest
Prompt: Extract the tag_name from this GitHub releases API response. Return just the tag name string.
```

If no releases found, show this error:
```
Error: No releases found for {owner}/{repo}

Plugins must have at least one tagged release.
Create a release at: https://github.com/{owner}/{repo}/releases/new
```

Store the tag name as `releaseTag` (e.g., `v1.0.0`).

### Step 4: Validate Repository Requirements

#### Check README exists
Use WebFetch:
```
URL: https://raw.githubusercontent.com/{owner}/{repo}/{releaseTag}/README.md
Prompt: Confirm this README.md file exists and has content. Return "exists" if it does.
```

If README not found:
```
Error: No README.md found in {owner}/{repo}

A README.md file is required with:
- What the plugin does
- Installation instructions
- Usage examples
```

#### Check LICENSE exists
Use WebFetch:
```
URL: https://api.github.com/repos/{owner}/{repo}/license
Prompt: Extract the license type from this response. Return the license name/spdx_id.
```

If LICENSE not found:
```
Error: No LICENSE file found in {owner}/{repo}

A LICENSE file is required. Recommended: MIT license.
```

### Step 5: Check for Duplicates

Read the current marketplace.json file and check if a plugin with the same `name` already exists.

```
Use Read tool: .claude-plugin/marketplace.json
```

If a plugin with the same name exists:
```
Error: A plugin named "{name}" already exists in the marketplace.

Existing entry:
  Repository: {existing repo}
  Version: {existing version}

If this is an update, edit the existing entry instead.
```

### Step 6: Generate Plugin Entry

Create the new plugin entry object:

```json
{
  "name": "{from plugin.json}",
  "source": {
    "source": "github",
    "repo": "{owner}/{repo}",
    "ref": "{releaseTag}"
  },
  "description": "{from plugin.json}",
  "version": "{from plugin.json, should match release}",
  "author": {
    "name": "{from plugin.json}",
    "email": "{from plugin.json, if present}"
  },
  "keywords": ["{from plugin.json, if present}"],
  "license": "{from plugin.json}",
  "type": "{from plugin.json}"
}
```

Notes:
- Include `author.email` only if present in plugin.json
- Include `keywords` only if present in plugin.json (as array)
- The `version` should come from plugin.json, not the release tag

### Step 7: Add to Marketplace

Use the Edit tool to add the new plugin entry to `.claude-plugin/marketplace.json`.

Add the new entry to the `plugins` array. Maintain proper JSON formatting with 2-space indentation.

### Step 8: Update README.md

Update the "Available Plugins" table in README.md to include the new plugin.

Read the README.md file and find the table under "## Available Plugins". The table format is:

```markdown
| Name | Description | Type | Repository |
|------|-------------|------|------------|
```

Add a new row for the plugin:

```markdown
| [{name}](https://github.com/{owner}/{repo}) | {short description} | {type} | [{owner}/{repo}](https://github.com/{owner}/{repo}) |
```

Notes:
- If the table contains the placeholder row `| *None yet* | *Be the first to submit a plugin!* | - | - |`, remove it before adding the new plugin
- Keep the description concise (truncate if longer than 60 characters)
- Sort entries alphabetically by name if there are multiple plugins

### Step 9: Validate JSON

Run validation to ensure the JSON is valid:

```bash
python3 -m json.tool .claude-plugin/marketplace.json > /dev/null && echo "Valid JSON"
```

If validation fails, fix the JSON formatting issue and retry.

### Step 10: Auto-Commit

Stage and commit the changes:

```bash
git add .claude-plugin/marketplace.json README.md
git commit -m "feat: add plugin {name}"
```

### Step 11: Success Output

Display a success message:

```
Successfully added plugin to marketplace!

Plugin: {name}
Repository: {owner}/{repo}
Version: {version}
Type: {type}

The change has been committed. To submit:
1. Push your branch: git push
2. Create a Pull Request to the main repository
```

## Error Handling Summary

| Error | Cause | Solution |
|-------|-------|----------|
| No plugin.json | File missing in repo | Add plugin.json to repo root |
| Missing fields | plugin.json incomplete | Add required fields |
| No releases | No tagged releases | Create a GitHub release |
| No README | README.md missing | Add README.md to repo |
| No LICENSE | LICENSE file missing | Add LICENSE file |
| Duplicate name | Plugin already exists | Update existing entry instead |
| Invalid JSON | Malformed marketplace.json | Fix JSON syntax |

## Example Session

User runs: `/add-plugin anthropics/example-plugin`

1. Parse: owner=`anthropics`, repo=`example-plugin`
2. Fetch plugin.json from `https://raw.githubusercontent.com/anthropics/example-plugin/HEAD/plugin.json`
3. Get latest release tag: `v1.2.0`
4. Verify README.md exists
5. Verify LICENSE exists
6. Check no duplicate in marketplace.json
7. Add entry to marketplace.json
8. Update README.md plugins table
9. Validate JSON
10. Commit changes
11. Show success message
