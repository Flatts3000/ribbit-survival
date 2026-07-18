# Security Policy

## Supported Versions

Ribbit Survival is pre-release (alpha); only the latest commit on `main` is supported. Once stable releases are published, this section will be updated with a version table.

## Reporting a Vulnerability

If you discover a security vulnerability in the Ribbit Survival pack, **please do not open a public issue.** Use one of these private channels:

1. **GitHub Security Advisories** (preferred): visit the repo's [Security tab](https://github.com/Flatts3000/ribbit-survival/security/advisories/new) and submit a draft advisory. This routes directly to the maintainer.
2. **Direct contact**: message the maintainer via the GitHub profile at [@Flatts3000](https://github.com/Flatts3000).

## What Counts

A modpack's threat surface is small but non-empty. Ribbit Survival ships only a packwiz manifest plus config overrides (no KubeJS scripts, no datapacks), so the realistic concerns are:

- **Supply chain** - a mod's `.pw.toml` entry pointing to the wrong jar (CDN poisoning, typo-squatted slug, a hash that doesn't match the intended file).
- **Malicious config overrides** - a shipped `config/` file that changes a mod's behavior in a way that harms a server or client beyond the intended pack tuning.
- **Server crashes / denial of service** - pack content (configs, the specific mod set + versions) that causes a server to crash or hang on specific player actions.
- **Resource exhaustion** - a pack-introduced config combination that produces loops or unbounded data structures that exhaust memory or CPU.

### What is NOT in scope here

These belong upstream - file with the relevant project, not this repo:

- A vulnerability in a bundled mod's own code -> that mod's issue tracker.
- A vulnerability in Productive Frogs -> [productive-frogs/security/advisories/new](https://github.com/Flatts3000/productive-frogs/security/advisories/new).
- A NeoForge / Minecraft client or server vulnerability -> NeoForge / Mojang.

If you're unsure whether something qualifies, report it privately to us and we'll route it.

## Response Timeline

- **Acknowledgement**: within 7 days of receiving the report.
- **Initial assessment**: within 14 days.
- **Fix + disclosure**: timing varies by severity. Critical issues get a hotfix release on CurseForge; lower-severity issues land in the next regular release.

This is a hobby OSS project - timelines are best-effort, not contractual.

## Disclosure

We follow coordinated disclosure: report privately, we work on the fix, and we publish the advisory + fix together. We'll credit the reporter unless you request anonymity.
