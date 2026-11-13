---
name: debt-relief-regulatory-digest
description: Build a sourced, shareable HTML digest of recent regulatory and enforcement actions that matter to debt relief, debt settlement, credit counseling, debt collection, credit repair, student loan relief, telemarketing, and lead generation, drawn from the FTC, CFPB, FCC, state attorneys general, and state financial regulators. Use whenever the user asks what regulators have done lately, wants an enforcement roundup or regulatory update, asks "anything new from the FTC / CFPB / state AGs", wants to know what regulators are flagging in debt relief marketing, telemarketing, or lead gen, or is preparing a compliance briefing, newsletter section, or post about recent enforcement, even if they never say "digest".
compatibility: Requires web search and web fetch, plus the ability to write a file (or publish an HTML artifact).
---

# Debt Relief Regulatory Action Digest

Federal enforcement in consumer finance has pulled back, and state attorneys general and state financial regulators have picked up much of the slack. The signal operators need is now scattered across dozens of agency pages. This skill finds those actions, verifies them against the primary record, labels each one honestly by its legal stage, translates it into concrete checks for the reader's own business, and delivers the result as a clean, self-contained HTML page that can be shared as-is.

It summarizes public records. It is not legal advice, and every output says so prominently.

## Inputs

Use these defaults unless the user specifies otherwise. Ask a question only if the request is genuinely ambiguous.

- **Window:** the last 30 days, counted back from today's date.
- **Audience:** `operators` (default) means debt relief, settlement, and credit counseling companies and their compliance teams. `partners` means lenders, EAPs, financial wellness platforms, affiliates, and publishers who refer consumers to those companies. The audience changes how the "What to check" notes are written.
- **Focus (optional):** advertising claims, telemarketing (TCPA/TSR), advance fees, licensing, lead gen and data practices, or collection.
- **States (optional):** prioritize or limit to specific states.

## Scope

**Core:** government actions against, or rules aimed at, debt relief and debt settlement, credit counseling and debt management, credit repair, student loan debt relief, debt collection, and the telemarketers and lead generators that serve them.

**Adjacent:** government actions in other consumer finance areas (lending, auto, lease-to-own, payments) only when the practice at issue is one a debt relief operator could easily repeat: deceptive advertising, misleading disclosures, telemarketing and robocall violations, consent and lead-data misuse, hidden or add-on fees, or unlicensed activity. These go in a separate Adjacent section.

**Excluded:**
- **Private litigation.** Class actions, individual TCPA suits, and private settlements are not regulatory actions, even when they involve telemarketing. They dominate search results for telemarketing topics, so filter them out deliberately. The only exception is a court ruling in a private case that changes how a rule is interpreted; that goes in Rules & guidance.
- General political news about agencies (budgets, leadership, litigation over an agency's existence) unless it directly changes a rule operators must follow.
- Anything announced outside the window, even if it is still being covered in the news.

## Research process

### 1. Discover

Run separate searches per agency and per practice; a single combined query returns shallow results. Include the current month and year in queries.

**Federal:** FTC press releases and case pages, CFPB enforcement actions, FCC enforcement and TCPA orders, and the Federal Register for final rules.

**State attorneys general:** search AG press releases by practice (debt relief, debt settlement, telemarketing, lead generation, collection). Multistate settlements are usually announced by several AGs on the same day.

**State financial regulators (do not skip this step):** many debt relief actions are licensing and consent orders that only appear on a state banking or financial regulator's own enforcement page or weekly bulletin, never in the news. Search each regulator directly, for example `[regulator name] enforcement orders [month year]` or `[regulator name] bulletin debt negotiation`. Always check the states the user names, then at minimum: California DFPI, New York DFS, Connecticut Department of Banking, Illinois IDFPR, Washington DFI, Texas OCCC, Florida OFR, and the Massachusetts Division of Banks. Note which ones you checked.

**Discovery sources (never cited as the sole source):** law-firm enforcement roundups and newsletters, and trade and financial press. Use them only to find actions, then go to the primary record.

### 2. Verify

For every candidate action, fetch the primary record and confirm:
- the announcement or publication date falls inside the window (an order signed just before the window but first published inside it counts; record both dates)
- every agency involved, and every state in a multistate action
- the respondent's name exactly as the agency states it
- the stage (step 3)
- the practice at issue and any monetary relief

**Which primary record controls:** the order, judgment, or complaint itself outranks the agency's press release. Press releases sometimes round, summarize, or describe the figures differently. When the order is available (agencies usually link it from the press release or case page), fetch it and take figures from it. If the order and the press release disagree, use the order's figure and add a one-line note in that entry showing both. If you could not open the order, use the press release figure and say so in the entry.

If you cannot find any primary record, put the item in the "Unverified" section with its secondary link, or drop it. Never present a secondary summary as a confirmed fact.

### 3. Label the stage

The stage determines what you are allowed to say. This is the most important rule in the skill, because getting it wrong misstates the legal record and exposes whoever shares the digest.

| Stage | What it means | How to write it | Badge class |
|---|---|---|---|
| Investigation | Announced subpoena, CID, or inquiry | "is investigating", "issued a CID to" | `stage-investigation` |
| Complaint filed | Lawsuit or administrative complaint | "alleges", "the complaint claims" | `stage-complaint` |
| Temporary order | TRO, preliminary injunction, temporary cease-and-desist | "a court temporarily halted", "issued a temporary order" | `stage-complaint` |
| Settlement / consent order | Agreed resolution | "agreed to settle"; add "without admitting or denying" only if the record says so | `stage-settlement` |
| Default judgment | Defendant did not respond; the court treats the allegations as true without them being contested | "the court entered a default judgment"; describe the conduct as alleged in the complaint, and add the note "Entered by default: the defendants did not contest the allegations." | `stage-default` |
| Judgment / final order | Decided on the merits by a court or after an administrative hearing | "the court found", "was ordered to" | `stage-judgment` |
| Rule / guidance | Not enforcement | goes in Rules & guidance | `stage-rule` |

Never write that a company "broke the law", "scammed", or "defrauded" anyone unless a court has found it on the merits, and even then use the court's own framing.

### 4. Tag the practice

Use one or more: `advance fees`, `advertising claims`, `telemarketing`, `consent & lead data`, `licensing`, `disclosures`, `collection conduct`, `fees & add-ons`, `impersonation`, `consumer funds`, `data security`, `other`.

### 5. Deduplicate

A multistate action is one entry listing all participating states (or the lead states plus a count). A follow-on development in a case already covered gets a one-line update that references the earlier stage.

### 6. Count every agency, including zeros

Build the agency ledger: one row for each agency or agency group you checked, with the number of in-scope actions found in the window, **including zero**. A zero is a finding. "CFPB: 0 new actions" tells the reader something the individual entries cannot, so never leave a checked agency out because nothing turned up. Agencies you did not check are not listed.

## Writing rules

- **Paraphrase.** Quote a source only when its exact wording matters, keep any quote under 15 words, and use no more than one quote per source.
- **Numbers come only from the record.** Do not compute totals or trends beyond simple counts of the items in this digest.
- **People.** Name companies as the agency names them. Prefer "the company's two managers" over individual names; name individuals only if the user asks and the primary record names them as respondents. Never include consumer details.
- **"What to check" notes are operational, not legal conclusions.** Write one or two checks the reader can run against their own business.
  - For **operators:** "Could any mailer or opening line be read as coming from a creditor or a government program?" "Is any fee collected before a debt is actually settled?"
  - For **partners:** "Does your referral page describe the partner's program in terms the partner can substantiate?" "Do you know how your partner obtains consent before calling referred consumers?"
- **Keep analysis separate.** Patterns go in the Top line, written as observations about this digest's items, not predictions.
- **Plain language.** Short sentences, sentence case, no hype.

## Output: an HTML page

Deliver the digest as one self-contained HTML file built from `assets/template.html`. Read the template first and follow it exactly; its comments mark which blocks repeat and which are optional.

1. Copy the template and fill every `{{PLACEHOLDER}}`. `{{AUDIENCE_PLAIN}}` is "debt relief operators and their compliance teams" or "referral partners (lenders, EAPs, affiliates, publishers)"; `{{FOCUS}}` is the focus or "all practices"; `{{COVERAGE_NOTE}}` lists the source types and state regulators checked, the counts included and unverified, and ends with "Coverage is not exhaustive." Repeat the marked blocks once per item, and delete any optional section that has no items (but never delete the coverage note, the agency ledger, the disclaimer, or the attribution).
2. Escape any `<`, `>`, and `&` that appear in source text. Put every source link in an `<a href>` with `rel="noopener"`.
3. Keep the **attribution** (the header credit and the footer credit to Dexter Weatherly, with the LinkedIn link) exactly as it appears in the template. It identifies who built the skill that produced the page.
4. Keep the **disclaimer** text exactly as written in the template, in both places it appears.
5. Name the file `regulatory-digest-YYYY-MM-DD.html` using today's date.
6. Deliver it the way the environment supports: publish it as an HTML artifact or present it as a file where those tools exist; otherwise save it to the working directory and tell the user the path.

After delivering the file, reply with no more than three lines: the window, how many actions are in it, and anything you could not verify.

## If the user wants content from the digest

If the user asks to turn the digest into a post, newsletter section, or briefing:
- Pick one action, or one pattern across several (the agency ledger is often the strongest angle), rather than summarizing everything.
- Open with the specific fact, then the operator or partner lesson.
- Keep the stage language exactly as in the digest. A post is where "alleged" most often gets dropped by accident.
- Put source links in a suggested first comment rather than the post body.
- Keep it B2B commentary, never consumer advice, and close with a short reminder that it isn't legal advice.

---
Skill created by Dexter Weatherly, linkedin.com/in/dexterweatherly
