# 🛡️ OpenClaw Skill Security

Security-first auditing for third-party OpenClaw skills. Protect your workspace from malicious or compromised skills.

**Two ways to use:**
1. **Quick start** — drop `SECURITY-AUDIT.md` into your AGENTS.md (simple rules)
2. **Full suite** — use the skill auditors for comprehensive protection

## Quick Start (Drop-in Rules)

Copy the contents of `SECURITY-AUDIT.md` into your `AGENTS.md`:

```bash
cat SECURITY-AUDIT.md >> ~/your-workspace/AGENTS.md
```

This gives you basic protection with manual audit rules.

## Full Auditor Suite

For comprehensive protection, use the skill-based auditors:

| Job | Skill | What it does |
|-----|-------|-------------|
| **Audit a skill** | `skill-auditor` | Vet any SKILL.md before install (typosquatting, permissions, prompt injection, supply chain, exfiltration) |
| **Audit your setup** | `setup-auditor` | Check your environment for credential leaks, unsafe defaults, missing sandbox |

### Audit a skill before installing

Load `skill-auditor` and give it the target:

```
1) Paste skills/skill-auditor/SKILL.md into your agent
2) Paste the target skill's SKILL.md
3) Ask: "Audit this skill. Return a SKILL AUDIT REPORT."
```

The auditor runs a 6-step protocol: metadata & typosquat check → permission analysis → dependency audit → prompt injection scan → network & exfiltration analysis → content red flags.

**Verdict:** SAFE / SUSPICIOUS / DANGEROUS / BLOCK

### Audit your environment

Load `setup-auditor` and answer wizard questions about your workspace:

```
1) Paste skills/setup-auditor/SKILL.md into your agent
2) Answer the wizard: workspace path, host agent, permissions, sandbox, ports
3) Get a SETUP AUDIT REPORT with a fix checklist
```

**Verdict:** READY / RISKY / NOT_READY

### Install into your host agent

- **Codex CLI:** `ln -s "$PWD/skills/skill-auditor" ~/.codex/skills/skill-auditor`
- **Claude Code:** `ln -s "$PWD/skills/skill-auditor" .claude/skills/skill-auditor`
- **No tooling:** paste the SKILL.md content into your LLM chat

## Why This Matters

Third-party skills can run arbitrary code on your machine. A compromised skill could:
- Exfiltrate API keys and secrets
- Modify your system configuration
- Install backdoors via dependency chains
- Phone home to external servers

## Threat Coverage

Both auditors together cover **12/12 real-world attack types** observed in the wild (including the ClawHavoc campaign):

| # | Attack type | skill-auditor | setup-auditor |
|---|------------|:---:|:---:|
| T1 | Typosquatting | ✓ | |
| T2 | Credential theft | | ✓ |
| T3 | Crypto miners | | ✓ |
| T4 | Reverse shells | ✓ | ✓ |
| T5 | Prompt injection | ✓ | |
| T6 | Skill loader exploits | ✓ | ✓ |
| T7 | Obfuscated commands | ✓ | |
| T8 | Supply chain attack | ✓ | |
| T9 | Social engineering | ✓ | |
| T10 | Persistence | | ✓ |
| T11 | Over-privilege | ✓ | ✓ |
| T12 | Data exfiltration | ✓ | ✓ |

Full evidence: [docs/threat-coverage-matrix.md](docs/threat-coverage-matrix.md)

## What's Inside

```
SECURITY-AUDIT.md           — Quick drop-in rules for AGENTS.md

skills/
  skill-auditor/SKILL.md    — Vet any skill (6-step protocol)
  setup-auditor/SKILL.md    — Audit your environment (wizard + 4-step)
  config-hardener/           — Harden OpenClaw config
  credential-scanner/        — Scan workspace for leaked secrets
  dependency-auditor/        — Supply chain / install hooks
  incident-responder/        — Post-incident playbook
  network-watcher/           — Network/exfil checks
  output-sanitizer/          — Redact secrets/PII from output
  permission-auditor/        — Permission fit + dangerous combos
  prompt-guard/              — Prompt injection detection
  sandbox-guard/             — Docker sandbox profiles
  skill-guard/               — Runtime monitoring checklist
  skill-vetter/              — Legacy deep audit checklist

docs/
  threat-coverage-matrix.md  — Which checks catch which attacks
  config-hardening-checklist.md — Minimum security baseline
  incident-response-playbook.md — What to do if compromised
```

## Report a Malicious Skill

Found something suspicious? [Open an issue](https://github.com/wiziswiz/openclaw-skill-security/issues/new) with sanitized evidence (no secrets).

## Credits

Built by the OpenClaw community:
- **Don** ([@defi69don](https://x.com/defi69don)) — original framework
- **JB** ([@bryptobricks](https://x.com/bryptobricks)) — network monitoring, version pinning, update diffing
- **wiz** ([@wiziswiz](https://x.com/wiziswiz)) — integration and publishing
- **UseClawPro** — skill modules and threat coverage

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

MIT — use it, share it, improve it.
