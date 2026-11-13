# Upload instructions (for the Claude instance publishing this repo)

You've been handed this folder to publish to Dexter's GitHub. Follow these steps in order. Don't change any file contents except where a step says to.

## Before you start — fill these in

| Value | What to use |
|---|---|
| `<OWNER>` | Dexter's GitHub username or org. Ask if you weren't given it. |
| `<REPO>` | Suggested: `debt-relief-regulatory-digest`. Use whatever name Dexter gave you. |
| Visibility | **Public** unless Dexter said private. The license (CC BY 4.0) assumes it will be shared. |
| New or existing repo | If Dexter named an existing repo, use the "existing repo" path in step 3. |

Prerequisites: `git`, and either the `gh` CLI authenticated to Dexter's account or a remote URL you have push access to. Never paste tokens into files or commit messages.

## 1. Sanity-check the folder

From the folder root, confirm these files exist:

```bash
ls README.md LICENSE CHANGELOG.md UPLOAD_INSTRUCTIONS.md .gitignore .gitattributes
ls skills/debt-relief-regulatory-digest/SKILL.md skills/debt-relief-regulatory-digest/LICENSE skills/debt-relief-regulatory-digest/assets/template.html
```

Check that `SKILL.md` starts with YAML frontmatter containing `name: debt-relief-regulatory-digest`:

```bash
head -5 skills/debt-relief-regulatory-digest/SKILL.md
```

If anything is missing, stop and report it rather than recreating it.

## 2. Initialize git and commit

Skip `git init` if a `.git` folder already exists.

```bash
git init -b main
git add .
git commit -m "Initial release: Debt Relief Regulatory Digest skill v1.0.0"
```

## 3. Create the GitHub repo and push

**New repo (with `gh`):**

```bash
gh repo create <OWNER>/<REPO> --public --source=. --remote=origin \
  --description "Claude skill: sourced HTML digest of FTC, CFPB, FCC, state AG and state regulator actions affecting debt relief, collection, telemarketing and lead gen." \
  --push
```

**New repo (without `gh`):** create an empty repo named `<REPO>` on github.com (no README, no license, no .gitignore — this folder already has them), then:

```bash
git remote add origin https://github.com/<OWNER>/<REPO>.git
git push -u origin main
```

**Existing repo:** clone it, copy this folder's contents into it (into a subfolder if the repo holds other things — ask Dexter which), then commit and push on a new branch and open a PR rather than pushing straight to `main`:

```bash
git checkout -b add-regulatory-digest-skill
git add . && git commit -m "Add Debt Relief Regulatory Digest skill"
git push -u origin add-regulatory-digest-skill
gh pr create --fill
```

## 4. Repo settings (new repo only)

```bash
gh repo edit <OWNER>/<REPO> \
  --add-topic claude --add-topic claude-skills --add-topic agent-skills \
  --add-topic debt-relief --add-topic compliance --add-topic regulatory \
  --homepage "https://www.linkedin.com/in/dexterweatherly/"
```

## 5. Optional: tag a release with an installable zip

Claude.ai installs skills from a zip whose root is the skill folder. Build it and attach it to a release:

```bash
cd skills && zip -r ../debt-relief-regulatory-digest.zip debt-relief-regulatory-digest && cd ..
git tag v1.0.0 && git push origin v1.0.0
gh release create v1.0.0 debt-relief-regulatory-digest.zip \
  --title "v1.0.0" --notes "Initial release. Download the zip and upload it in Claude under Settings → Capabilities → Skills."
```

Don't commit the zip itself; `.gitignore` already excludes `*.zip`.

## 6. Verify and report back

- Open `https://github.com/<OWNER>/<REPO>` and confirm the README renders and `skills/debt-relief-regulatory-digest/SKILL.md` is present.
- Report to Dexter: the repo URL, visibility, the commit hash, and the release URL if you made one.

## Don'ts

- Don't edit `SKILL.md`, `template.html`, or either `LICENSE` file.
- Don't remove the attribution or disclaimer blocks from the template.
- Don't add sample digests that name individuals or include consumer details.
- Don't commit credentials, `.env` files, or tokens.
