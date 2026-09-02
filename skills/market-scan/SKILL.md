---
name: market-scan
description: Build a rubric-based competitive market scan comparing several vendors/products in a technology category for senior leadership — a weighted feature rubric with confidence-tagged ratings, an internal pipeline/relationship signal overlay where available, packaged as an executive summary + market landscape + per-vendor deep dives + strategic recommendation, published as a deck or report. Use when asked for a market scan, vendor scan, competitive scan, OEM/vendor comparison, or "how do these N vendors stack up" naming a technology category and a shortlist of vendors.
---

# Market Scan

## Overview

Given a technology category (e.g. an acronym or emerging market name) and a shortlist of vendors,
produce a structured competitive scan: a feature-by-feature rubric with confidence-tagged ratings,
an internal signal overlay (Salesforce pipeline, ATC lab/demo status) kept separate from the
objective score, and an executive-ready package (summary, market landscape, per-vendor deep dives,
strategic recommendation).

First built this way for the 2026-05 "AEV" (Adversarial Exposure Validation) market scan — a
4-vendor comparison authored for an SVP-level stakeholder — and again six weeks later as a
lightweight "market update" re-scoring what moved. This skill generalizes that methodology; it does
not reproduce that scan's actual vendor ratings, which are WWT-internal competitive intelligence.

## Workflow

1. **Scope the category.** Name the category plainly (spell out any acronym on first use). Pick a
   **focal vendor set** — the 3-5 vendors the stakeholder actually needs a verdict on — and, if
   useful for context, a broader **landscape cohort**: adjacent or emerging players grouped into
   2-4 named clusters (e.g. by architecture or go-to-market approach) rather than individually
   scored. Confirm the focal set and the decision this scan is meant to inform before building the
   rubric — a scan built to pick a technical standard looks different from one built to flag an
   investment/partnership risk.

2. **Build the rubric.** Identify 5-8 capability categories relevant to the technology (e.g. for a
   security-tooling category: something like realism/depth of the core technique, autonomy/AI
   maturity, time-to-value and production safety, integration and reporting — the actual categories
   depend entirely on what the stakeholder cares about). Break each category into specific,
   independently-verifiable features. Score every feature on a fixed scale, for example:
   **Market Leading / Mature / Functional / Minimally Viable / Non-viable / Not Implemented.**
   Reuse the same scale across every vendor in the scan — the rubric only has value if the bar is
   identical for all of them.

3. **Tag every rating with a confidence level (High/Low),** tied to evidence quality, not to how
   favorable the rating is:
   - High confidence: public documentation, published benchmarks, a hands-on evaluation, or a
     named customer reference confirms the rating.
   - Low confidence: the rating rests on vendor claims, an architecture pitch, or a single
     secondhand account.
   Score young or stealth-adjacent vendors conservatively and mark them Low confidence rather than
   extrapolating a generous rating from limited evidence — the credibility of the whole scan rides
   on this discipline, especially when a vendor's backers or narrative are impressive but the
   evidence base is thin.

4. **Gather evidence per vendor.** For 4 or more focal vendors, launch one subagent per vendor, all
   in a single message (see `references/fork-prompt-templates.md`), to score its vendor against the
   full rubric with a citation per rating, write a 2-4 sentence company narrative (differentiation,
   funding/backing, and the biggest evidence gap), and pull WebSearch/Glean/analyst-note evidence
   as needed. For 1-3 vendors, do this research directly yourself — the parallel-fork overhead only
   pays off once there's enough surface area for a QA pass to be worth running.

5. **Overlay internal signal separately.** If any focal vendor is a partner WWT already carries
   pipeline on, pull it as its own section — Salesforce closed-won/active opportunities, ATC lab or
   demo status, named account team relationships — and keep it visibly separate from the rubric
   score. "What our own pipeline shows" and "what the market/technical evidence shows" are two
   different questions; a vendor can be commercially ahead while scoring lower on the rubric, or
   vice versa, and collapsing the two into one number hides that tension instead of surfacing it.
   Skip this step entirely (don't pad the report with "no internal signal found") for any vendor WWT
   has no relationship with yet.

6. **Run a QA pass** once per-vendor research is back (template in
   `references/fork-prompt-templates.md`): check the rubric was applied consistently (did one
   vendor get a generous read on a feature that another with equivalent evidence did not?),
   recompute every rollup (category-by-category tally, total score) from the individual ratings
   rather than trusting a hand-added sum, verify any internal-signal figures against a live query,
   and flag any place the drafted narrative states a Low-confidence rating as settled fact. Use
   QA's corrected numbers and language, not the pre-QA draft.

7. **Package the scan.** Structure:
   - **Executive summary** — the headline verdict in one sentence, plus 2-3 stat-callout takeaways
     (e.g. a total score, a category-win tally, a standout metric).
   - **Market landscape** — the broader cohort view for context, grouped by the clusters from step 1.
   - **Per-vendor deep dives** — one section per focal vendor: the rubric table (rating + confidence
     per category), the narrative, and the internal-signal callout if one exists.
   - **Strategic recommendation** — what the stakeholder should actually do (standardize, pilot,
     productize, wait for more evidence), stated plainly.
   - **Named next step** — the single highest-leverage action that would close the biggest
     remaining evidence gap (e.g. a technical deep-dive with a specific team), not a generic list.
   - **Appendix** — the full rubric and the confidence-tagging rule, so a skeptical reader can
     audit any individual rating.

8. **Choose the output format for the audience.** A single SVP-level review sitting usually wants a
   deck (PowerPoint or Gamma); an artifact meant to be referenced or shared more widely over time is
   better as an HTML report on `my-pages.apps.wwt.com` in Wire style (see
   `[[wire-personal-style]]` / `personal-style/template.html`). Ask if it's unclear which. Mark
   sensitivity deliberately — a scan naming specific vendors' competitive weaknesses or WWT's own
   forward GTM thinking is often restricted-eligible even when the underlying market facts are
   public.

9. **Offer a follow-up cadence.** A market moves faster than a one-time scan stays accurate. Offer
   a lightweight "market update" a few weeks out that only re-scores what changed: a table of
   vendor / prior position / what moved / new read, tied back to the original scan's thesis and
   whatever decision was left open. Keep this brief — it's a delta, not a redo of the full rubric.

## Notes

- This is research and synthesis, not a data-entry exercise — the rubric only earns trust if every
  rating is backed by a real citation and the confidence tag is honest about the ones that aren't.
- Don't let AI-accelerated drafting substitute for validation: have ratings checked against account
  teams or technical subject-matter experts who actually know the vendors before the scan goes to a
  senior stakeholder, the same way the QA pass checks arithmetic.
- Before publishing anything with hand-placed record links or dollar figures pulled from an internal
  system, cross-check them against the source data directly (see `[[verify-record-ids-before-
  publish]]`) rather than trusting a subagent's summary verbatim.
- A scan built for an internal, WWT-specific decision (which OEM to standardize on, whether to
  invest in a partnership) is different from one meant as neutral external analysis — say which one
  this is up front, since it changes how directly the recommendation should be stated.
