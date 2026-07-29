---
name: seo-portfolio-update
description: Update the AI-automation SEO portfolio page with fresh account data, add a new account, or refresh numbers before sending it to a new employer. Commits and pushes to GitHub.
---

# SEO Portfolio: Update

Update `ai-automation-portfolio.html`, the job-application portfolio page covering client accounts organized by AI-automation tier (n8n pipelines, Claude Code skills, supporting data tooling).

## Step 1: Confirm scope

Ask what this update is for:
- Refreshing numbers on an existing account (which one, and why: new export, more recent month, etc.)
- Adding a new account
- General cleanup pass before sending the link to a specific employer

## Step 2: Identify what data is missing

For the account(s) in scope, check what's already in the page versus what's needed:
- **GA4**: Traffic acquisition report, Organic Search (+ Organic Social if relevant) channel, grouped by month. Tenure split is **Jul–Dec 2025 vs. Jan–Jun 2026** (Josette joined WebProfits July 2025) unless the account's actual start date is later, ask if unsure.
- **GSC**: Performance on Search export (zip with Chart/Queries/Pages CSVs), monthly breakdown.
- **DataForSEO**: use `dataforseo_query.py` in the account's own folder under `/Users/josette/Desktop/Claude/` if a ranked-keywords or domain-overview check is needed. **Always pass the correct location code for the account's actual market** (e.g. Australia = 2036, not the library default of 2840/USA) and the correct domain (check the live site's actual URLs, e.g. via a GSC export, rather than assuming from an old report). A past diagnostic for Satellite Office got both wrong and produced numbers that didn't hold up.
- Check `/Users/josette/Downloads/` for exports the user may have already pulled this session before asking for anything new.

Ask for exactly what's missing, specifying the exact report type, channel, and date range needed, don't ask vaguely for "more data."

## Step 3: Never fabricate

This is a factual, job-application document. Every number must trace to a real export or a script pull, not an estimate or a plausible-sounding round figure.

- If an account has no real data yet (e.g. content built but unpublished), say so in the copy. Look at the Satellite Office and Investment Markets sections for the established honest-caveat pattern.
- If a trend is mixed or negative, show it. Look at the Morrisons Law and ATA Scientific sections for the established pattern of presenting flat or declining numbers honestly alongside the wins.
- Don't cherry-pick a favorable date range that a full trend table right next to it would contradict.

## Step 4: Match the existing format

Every account section follows the same structure, keep new/updated sections consistent:
- `<p class="eyebrow accent">` client name
- `<h3>` one-line description
- `<p class="tenure">` context line
- `<p class="lede">` framing paragraph
- Optional `<div class="hero-stat">` for one standout number, only if there's a real, defensible headline stat, don't force one (see Morrisons Law for a section with no hero-stat)
- `<h4 class="label">Organic search, first half of tenure vs. second half</h4>` + `.stat-grid` of 4 tiles (sessions, engagement rate, leads, lead rate: adapt to ecommerce metrics like Beauty Chef/SharkNinja if the account has revenue)
- `<p class="table-foot">` source line
- `<p class="caveat">` honest interpretation, including any negative or flat context

Reuse the existing CSS classes already defined in the file, don't introduce new component styles for a single section.

## Step 5: Update the "At a glance" table

If output/status changed for the account, update its row in the overview table near the top of the page too, keep it in sync with the detail section.

## Step 6: Em-dash check

Before finishing, grep the file for all four patterns and confirm zero:
```bash
FILE="/Users/josette/Desktop/Personal/SEO Portfolio/repo/ai-automation-portfolio.html"
grep -c "—" "$FILE"; grep -c "&mdash;" "$FILE"; grep -c "&#8212;" "$FILE"; grep -c "&#x2014;" "$FILE"
```
All four must return 0.

## Step 7: Commit and push

```bash
cd "/Users/josette/Desktop/Personal/SEO Portfolio/repo"
gh auth switch --hostname github.com --user jdbartolome0023
git add ai-automation-portfolio.html
git commit -m "[account]: [what changed]"
git push origin main
```

`index.html` in this repo is the separate Mattek interview follow-up page, never touch it as part of this workflow.

## Step 8: Confirm

Report:
- What changed and which account(s)
- The live URL: https://jdbartolome0023.github.io/seo-portfolio-reports/ai-automation-portfolio.html
- Any account still missing data, so it's not forgotten next time
