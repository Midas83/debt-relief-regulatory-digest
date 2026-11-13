# Debt Relief Regulatory Digest — a Claude skill

A [Claude Agent Skill](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview) that builds a sourced, shareable HTML digest of recent regulatory and enforcement actions that matter to debt relief, debt settlement, credit counseling, debt collection, credit repair, student loan relief, telemarketing, and lead generation.

It pulls from the FTC, CFPB, FCC, state attorneys general, and state financial regulators, verifies each action against the primary record, labels it honestly by legal stage, and turns it into concrete "what to check" notes for your own business.

> **Not legal advice.** The skill summarizes public records. Every digest it produces says so prominently.

## Why it exists

Federal enforcement in consumer finance has pulled back, and state AGs and state financial regulators have picked up much of the slack. The signal is now scattered across dozens of agency pages and weekly bulletins that never make the news. This skill does the legwork and produces one clean page you can share as-is.

## What it does

1. **Discovers** actions with separate searches per agency and per practice — federal (FTC, CFPB, FCC, Federal Register), state AGs, and state financial regulators (CA DFPI, NY DFS, CT DOB, IL IDFPR, WA DFI, TX OCCC, FL OFR, MA Division of Banks, plus any states you name).
2. **Verifies** each one against the order, judgment, or complaint itself, which outranks the press release. Anything without a primary record goes in an "Unverified" section.
3. **Labels the stage** — investigation, complaint, temporary order, settlement, default judgment, final judgment, or rule — and writes accordingly. "Alleges" stays "alleges."
4. **Tags the practice** — advance fees, advertising claims, telemarketing, consent & lead data, licensing, disclosures, and more.
5. **Counts every agency checked, including zeros.** "CFPB: 0 new actions" is a finding.
6. **Writes "What to check" notes** for one of two audiences: `operators` (debt relief companies and their compliance teams) or `partners` (lenders, EAPs, affiliates, publishers who refer consumers).
7. **Outputs** one self-contained HTML page, `regulatory-digest-YYYY-MM-DD.html`, with light/dark mode, mobile layout, and print styles.

Private class actions and individual TCPA suits are excluded on purpose; they're not regulatory actions.

## Repository layout

```
.
├── README.md                     ← this file
├── LICENSE                       ← CC BY 4.0
├── CHANGELOG.md
├── UPLOAD_INSTRUCTIONS.md        ← steps for publishing this folder to GitHub
├── .gitignore
├── .gitattributes
└── skills/
    └── debt-relief-regulatory-digest/
        ├── SKILL.md              ← the skill: instructions + frontmatter
        ├── LICENSE
        └── assets/
            └── template.html     ← the HTML page the digest is built from
```

The `skills/debt-relief-regulatory-digest/` folder is the installable unit. Everything else is repo packaging.

## Install

### Claude.ai (web, desktop, mobile)

1. Zip the skill folder so the folder itself is at the root of the zip:
   ```bash
   cd skills && zip -r ../debt-relief-regulatory-digest.zip debt-relief-regulatory-digest
   ```
   (Or download the zip attached to the latest GitHub release, if there is one.)
2. In Claude, open **Settings → Capabilities → Skills**, choose **Upload skill**, and select the zip.
3. Make sure web search is enabled.

### Claude Code

Copy the skill folder into your personal or project skills directory:

```bash
# personal (all projects)
cp -r skills/debt-relief-regulatory-digest ~/.claude/skills/

# or project-only
cp -r skills/debt-relief-regulatory-digest .claude/skills/
```

### Claude API / Agent SDK

Upload the `skills/debt-relief-regulatory-digest/` folder through the Skills API, or point the Agent SDK at a directory that contains it. See Anthropic's [Agent Skills docs](https://docs.claude.com/en/docs/agents-and-tools/agent-skills/overview).

**Requirements:** web search, web fetch, and the ability to write a file or publish an HTML artifact.

## Use

You don't need to say "digest." Any of these will trigger it:

- "What have regulators done lately in debt relief?"
- "Anything new from the FTC or state AGs this month?"
- "Give me an enforcement roundup for our referral partners, focused on telemarketing."
- "Regulatory update for the last 60 days, prioritize California and New York."

**Defaults** (override in your request):

| Input | Default | Options |
|---|---|---|
| Window | Last 30 days | Any date range |
| Audience | `operators` | `operators`, `partners` |
| Focus | All practices | advertising claims, telemarketing (TCPA/TSR), advance fees, licensing, lead gen & data, collection |
| States | Core regulator list | Any states to prioritize or limit to |

After the digest, you can ask Claude to turn it into a LinkedIn post, newsletter section, or briefing. The skill keeps stage language intact ("alleged" stays in) and puts source links in a suggested first comment.

## Customizing

- **Look and feel:** edit `assets/template.html`. Keep the placeholders, the `REPEAT` / `OPTIONAL` comment markers, the disclaimer blocks, and the attribution blocks.
- **Scope or regulator list:** edit the *Scope* and *Research process* sections of `SKILL.md`.
- **Triggering:** the `description` in the `SKILL.md` frontmatter controls when Claude picks up the skill.

## License and attribution

Licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/). You may share and adapt it, including commercially, as long as you credit **Dexter Weatherly** ([LinkedIn](https://www.linkedin.com/in/dexterweatherly/)), link to the license, and note any changes.

The attribution and disclaimer blocks in the template are meant to stay in every generated digest.

## Disclaimer

This skill and its output summarize public records from government agencies. Nothing here is legal advice. Allegations in complaints and settlements are not findings of wrongdoing. Check with your attorney about how any ruling, order, or regulation applies to your business.

---

Created by [Dexter Weatherly](https://www.linkedin.com/in/dexterweatherly/).
