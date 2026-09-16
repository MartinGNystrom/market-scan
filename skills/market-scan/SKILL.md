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
lightweight "market update" re-scoring what moved. Reused and extended for the 2026-09 Xage
Security scan (5 vendors, serving an outside-investor request and an internal WWT
partnership-activation question at once), which added confidence-weighted scoring as a required
step rather than a nice-to-have, a category-definition section ahead of the executive summary, and
a self-contained positioning chart to the package. This skill generalizes that methodology; it does
not reproduce either scan's actual vendor ratings, which are WWT-internal competitive intelligence.

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
   has no relationship with yet — but if the scan's actual focal/subject vendor (the one the
   stakeholder is asking about) turns out to have zero internal signal, don't bury that in a
   one-line skip. A dormant or unenriched CRM account on the vendor everyone is asking about is
   often the single most decision-relevant fact in the whole scan — it belongs in the executive
   summary, not just tucked into that vendor's own subsection.

6. **Run a QA pass** once per-vendor research is back (template in
   `references/fork-prompt-templates.md`): check the rubric was applied consistently (did one
   vendor get a generous read on a feature that another with equivalent evidence did not? — pay
   particular attention to every feature where the honest answer is "no evidence found": every
   vendor with that same absence of evidence must land on the same default rating, not whatever
   tier each subagent happened to pick), recompute every rollup (category-by-category tally, total
   score) from the individual ratings rather than trusting a hand-added sum, verify any
   internal-signal figures against a live query, and flag any place the drafted narrative states a
   Low-confidence rating as settled fact — read the narrative against its own feature table, not in
   isolation, since a narrative can contradict a rating sitting one paragraph away. If several
   subagents all had to leave the same disclosure ambiguous (e.g. none could confirm whether a CRM
   dollar figure is gross profit or contract value), standardize that caveat to identical wording
   across every vendor in this pass rather than shipping five different phrasings of the same
   unresolved question. Use QA's corrected numbers and language, not the pre-QA draft.

7. **Compute a confidence-weighted score, not just a raw tally.** A raw sum (e.g. Market
   Leading=5 … Not Implemented=0, summed across every feature) counts an unverified vendor claim
   exactly the same as independently corroborated evidence — that materially overstates any vendor
   whose ratings lean Low-confidence. Discount every Low-confidence rating (50% is a reasonable
   default) and keep High-confidence ratings at full value, then rank on that number. This can
   reorder the raw ranking in ways worth calling out explicitly: in the 2026-09 Xage scan it dropped
   the scan's own subject vendor from a raw #3 to a confidence-weighted #4 of 5, swapping places
   with a better-evidenced competitor — a materially different story than the raw tally told on its
   own. Report the raw score too (the per-vendor deep dives are a natural place for both numbers
   side by side), but let the confidence-weighted number drive the report's actual conclusions and
   ranking language.

8. **Package the scan.** Structure:
   - **What is this market?** — a short category-definition section before the executive summary:
     why the category exists (what forces it into being), who buys it, and the 2-3 adjacent
     categories buyers commonly conflate it with. Skip only when the stakeholder is already a
     category expert; for anything investor-facing or cross-functional, don't assume the reader
     already knows what the category acronym or name actually means.
   - **Executive summary** — the headline verdict in one sentence, then exactly 3 stat-callout
     takeaways in the style of the original AEV scan: each a bolded claim-headline, a single big
     number, and 1-2 sentences of support, not a bare metric. The three takeaways should follow a
     fixed rhythm — the category's evidence leader, the vendor actually driving the stakeholder's
     ask (which is not always the leader), and WWT's own differentiated signal on that vendor (or
     its absence) — rather than four or five generic metrics. Keep every top-line stat a
     comparative market fact between vendors (funding, valuation, named federal/regulatory
     credentials, WWT pipeline dollars) rather than a statement about the analysis's own confidence
     or score; that self-referential framing belongs in supporting prose, the deep dives, and the
     appendix, not the headline callouts a reader sees first. Add a short attribution line under the
     stat grid (author, practice, "full rubric in appendix"), matching the AEV precedent.
   - **Market landscape** — the broader cohort view for context, grouped by the clusters from step
     1. A short 2x2 positioning chart (inline SVG, no external charting library, so the document
     stays self-contained) is worth adding when the stakeholder would benefit from a
     McKinsey/Gartner-style visual — but plot two purely factual, comparative axes (e.g. product
     architecture orientation vs. funding/valuation on a log scale), never an axis that scores "how
     well-evidenced" a vendor is, and invent neutral, axis-specific quadrant labels rather than
     reusing a specific analyst firm's trademarked terms (Leaders/Challengers/Visionaries/Niche
     Players are Gartner's, not generic). Name which vendors were actually scanned only where it
     changes what the reader should trust — the per-vendor deep dives and appendix already make
     that obvious, so an inline "(scanned)" / "(not scanned)" tag on every cluster-card vendor name
     reads as clutter, not clarity; a plain "X, alongside Y and Z" carries the same information.
   - **Per-vendor deep dives** — one section per focal vendor: the rubric table (rating + confidence
     per category), the narrative, and the internal-signal callout if one exists. Show both the raw
     score and the confidence-weighted score side by side here even when the executive summary only
     leads with the weighted one. Category-level rollups should average the underlying feature
     scores and round conservatively — a .5 average rounds down, not up.
   - **Strategic recommendation** — what the stakeholder should actually do (standardize, pilot,
     productize, wait for more evidence), stated plainly. When a single scan serves two audiences at
     once (e.g. a neutral read for an outside investor, and an internal WWT partnership-activation
     question), keep the two conclusions visibly separate — the neutral market findings drive one,
     WWT's own forward GTM thinking drives the other, and blending them into a single recommendation
     undermines the credibility of the external-facing read.
   - **Named next step** — the single highest-leverage action that would close the biggest
     remaining evidence gap (e.g. a technical deep-dive with a specific team), not a generic list.
   - **Appendix** — the confidence-tagging rule, the confidence-weighting formula, every QA
     correction actually made (with the reasoning), and the full per-feature rubric table for every
     vendor with a citation per rating — shipped in the document itself, not deferred to "available
     on request." A market scan's credibility rests on a skeptical reader being able to trace any
     claim in the report back to the specific rating it came from; a summary-only appendix breaks
     that chain.

9. **Choose the output format for the audience.** A single SVP-level review sitting usually wants a
   deck (PowerPoint or Gamma); an artifact meant to be referenced or shared more widely over time is
   better as an HTML report on `my-pages.apps.wwt.com` in Wire style (see
   `[[wire-personal-style]]` / `personal-style/template.html`). Ask if it's unclear which. Mark
   sensitivity deliberately — a scan naming specific vendors' competitive weaknesses or WWT's own
   forward GTM thinking is often restricted-eligible even when the underlying market facts are
   public.

10. **Offer a follow-up cadence.** A market moves faster than a one-time scan stays accurate. Offer
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
  this is up front, since it changes how directly the recommendation should be stated. When one scan
  has to do both jobs at once, keep the two conclusions in visibly separate sections rather than
  blending them into a single recommendation.
- Executive-summary stat callouts should read as market facts a reader could verify independently
  (funding, valuation, contract counts, pipeline dollars) — not as commentary on how confident this
  scan's own scoring is. Save the analysis-quality story (percent High-confidence, raw vs.
  confidence-weighted score) for supporting prose, the deep dives, and the appendix, where a reader
  who actually wants to audit the methodology can find it.
