# Fork/subagent prompt templates

Reuse the structure below, swap in the category, rubric, and vendor facts discovered during the
setup pass (Workflow steps 1-3 in `SKILL.md`).

## Per-vendor subagent prompt (one per focal vendor, launched together in a single message)

```
Score <Vendor Name> against the <Category> rubric below for a market scan aimed at <the decision
this scan informs, e.g. "deciding whether WWT standardizes on one vendor in this category">.

RUBRIC (reuse exactly — do not add, drop, or reword categories/features mid-scan):
<paste the fixed category/feature list and the rating scale, e.g. Market Leading / Mature /
Functional / Minimally Viable / Non-viable / Not Implemented>

YOUR JOB:
1. For every feature, assign a rating from the fixed scale AND a confidence tag (High/Low):
   - High confidence = backed by public documentation, a published benchmark, a hands-on
     evaluation, or a named customer reference.
   - Low confidence = resting on a vendor claim, an architecture pitch, or a single secondhand
     account.
   Cite the source for every rating (a URL, a document name, or "no evidence found — scored
   Non-viable/Low confidence by default"). Do not let a strong narrative or well-known backers
   inflate a rating with no direct evidence — score conservatively and mark Low confidence instead.
2. Write a 2-4 sentence company narrative: differentiation, funding/backing (WebSearch for
   funding/investor signals if not publicly traded — treat "no funding signal found anywhere" as
   its own finding, not a gap to skip), and the single biggest evidence gap for this vendor
   specifically.
3. If <Vendor Name> is a partner WWT already carries pipeline on, pull the internal-signal
   overlay separately from the rubric score: [CRM connector — resolve tool names with ToolSearch]
   partner status/tier, open + closed-won pipeline (state whether a dollar figure is gross profit
   or revenue — don't conflate the two), and ATC lab/demo status. If there's no WWT relationship,
   say so in one line and move on — don't pad the report with a boilerplate "not applicable" for
   every section.
4. Flag anything that looks like a name collision with an unrelated company, or evidence that
   conflicts with another public source, rather than silently picking one.

Return a concise structured report (rubric table + narrative + internal-signal callout, under
400 words). Do not write any files or publish anything — just report findings back in your final
message.
```

## QA subagent prompt (run whenever 2+ vendors are being compared)

```
QA pass on the compiled <Category> market scan covering <N> vendors: <list>. Here is the compiled
rubric data and internal-signal figures to verify:

<paste every vendor's per-feature ratings + confidence tags + citations, narrative, and any
internal-signal figures>

YOUR TASKS:
1. Consistency check: for each rubric feature, compare how it was scored across all vendors — flag
   any feature where one vendor got a more generous rating than another despite equivalent (or
   weaker) cited evidence. The rubric only has value if the bar was identical for everyone.
2. Recompute every rollup (category-by-category win tally, total score across all features) directly
   from the individual per-feature ratings — don't trust a hand-added sum. Show your math and flag
   any mismatch.
3. Confidence-language check: scan every narrative sentence for a Low-confidence rating being stated
   as settled fact (no hedge, no "reported," no "claims") — flag each instance and propose a
   corrected phrasing that keeps the hedge visible.
4. If any internal-signal figure was reported, re-run one live spot-check query per vendor and flag
   any drift from what was reported (data may have changed since the subagent ran).
5. Sanity-check for anything else internally inconsistent: a citation that doesn't actually support
   its rating, a vendor evaluated on a feature that doesn't apply to its architecture, a dollar
   figure mislabeled as gross profit vs. revenue.

Report back concisely (under 400 words): pass/fail on consistency and arithmetic, the confidence-
language findings, live-data spot-check results, and any other flags. This is a verification pass
only — do not rewrite the report itself. Apply QA's corrected numbers and language before writing
the final package, not the pre-QA draft.
```

## Notes from the first run (2026-05 AEV scan)

- AI accelerated the research, synthesis, and drafting — but ratings were still validated manually
  with account teams and technical subject-matter experts before the scan went to a senior
  stakeholder. Treat the subagent pass as a first draft the QA pass and human validation both need
  to touch, not a finished product.
- The scan named a single, specific "highest-leverage next step" (a technical deep-dive with a named
  team) as the critical unresolved risk, rather than a generic list of follow-ups. A stakeholder
  reading an executive summary needs one clear next action, not a backlog.
- A six-week-later "market update" brief re-scored only what moved — a compact table of vendor /
  prior position / what changed / new read — rather than rebuilding the full rubric from scratch.
  Keep that follow-up format ready; it's a natural cadence for any category that's still evolving
  when the original scan ships.
