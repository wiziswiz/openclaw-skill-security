# 🛡️ OpenClaw Skill Security Audit

Security hardening rules for installing third-party OpenClaw skills. Drop this into your AGENTS.md to protect your workspace from malicious or compromised skills.

## Quick Start

Copy the contents of `SECURITY-AUDIT.md` into your `AGENTS.md` file, or paste it directly:

```bash
cat SECURITY-AUDIT.md >> ~/your-workspace/AGENTS.md
```

## Why This Matters

Third-party skills can run arbitrary code on your machine. A compromised skill could:
- Exfiltrate API keys and secrets
- Modify your system configuration
- Install backdoors via dependency chains
- Phone home to external servers

These rules ensure every skill gets audited before it touches your system.

## Credits

Built by the OpenClaw community:
- **Don** ([@defi69don](https://x.com/defi69don)) — original framework
- **JB** ([@bryptobricks](https://x.com/bryptobricks)) — network monitoring, version pinning, update diffing, fetch() nuance fix
- **wiz** ([@wiziswiz](https://x.com/wiziswiz)) — integration and publishing

## License

MIT — use it, share it, improve it.
