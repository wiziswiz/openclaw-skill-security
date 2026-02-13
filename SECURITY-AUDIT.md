## External Skill Security Audit (MANDATORY)

Third-party skills are untrusted code. Before installing ANY new skill from ClawHub or external sources:

### Pre-install audit:
1. List ALL files in the skill (`find <skill-dir> -type f`)
2. Read EVERY script (.sh, .py, .js) — understand what it does
3. Check skill.json / SKILL.md metadata for install steps (npm install, pip install, brew install, etc.)
4. Check for external URLs, especially in install instructions — verify they point where they claim
5. Check allowed-tools — does the skill request more than it needs?

### Red flags — DO NOT install:
- Install steps that fetch from external URLs (curl, wget, fetch())
  - Note: fetch() in runtime scripts is fine for web tools/API integrators — the red flag is fetch in *install scripts* or to *unexpected domains*
- Obfuscated code or encoded payloads (base64, hex)
- npm install / pip install of unknown packages (check the package on npmjs.com/pypi first)
- Scripts that remove quarantine attributes (xattr -d)
- Requests for credentials, tokens, or env vars beyond what the skill needs
- "Required dependencies" that aren't in the official OpenClaw/system packages

### After install:
- Re-audit if the skill auto-updates
- Never run skill scripts with elevated permissions unless explicitly needed and approved
- **Post-install network monitoring**: on first run of any new skill, check for unexpected outbound connections
- **Pinned versions**: if a skill requires npm/pip packages, pin exact versions (not latest) to prevent supply chain attacks
- **Diff on updates**: if a skill updates, diff the changes before accepting — an innocent skill today could turn malicious in an update
