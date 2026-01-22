# Security Policy

## Supported Versions

As this is a plugin registry, "versions" refers to the registry itself. We generally support the latest version of the registry schema.

| Version | Supported          |
| ------- | ------------------ |
| latest  | :white_check_mark: |

## Reporting a Vulnerability

We take the security of this registry seriously. If you discover a security vulnerability, please bring it to our attention.

### Vulnerabilities in the Registry

If you find a vulnerability in the registry itself (e.g., in the schema, validation scripts, or CI/CD workflows), please report it to the maintainers.

**Do NOT report security vulnerabilities via public GitHub issues.**

Instead, please report them via:
* Email: security@modulabs.io
* GitHub Security Advisories (if enabled for this repository)

We will respond to your report within 48 hours.

### Vulnerabilities in Listed Plugins

**Disclaimer:** This repository is a registry of links to external plugins. We do not host the plugin code ourselves.

If you discover a vulnerability in a **specific plugin** listed in this marketplace:

1.  **Check the plugin's repository**: Go to the plugin's source repository (linked in the marketplace entry).
2.  **Report to the author**: Look for a `SECURITY.md` file or contact information in that repository.
3.  **Notify us (Optional)**: If a plugin is malicious or contains a critical unpatched vulnerability, please notify us so we can consider removing it from the registry to protect users. Open an issue with the label `security` or contact us privately.

### Malicious Plugins

If you believe a plugin listed here is intentionally malicious (malware, data exfiltration, etc.):

1.  Please report it immediately to us via security@modulabs.io or a private channel.
2.  Provide evidence of the malicious behavior.
3.  We reserve the right to remove any plugin from the registry at our discretion.
