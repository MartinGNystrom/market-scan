# Market Scan

A Claude Code plugin/skill for building a rubric-based competitive market scan: comparing several
vendors/products in a technology category against a fixed feature rubric with confidence-tagged
ratings, overlaying an internal pipeline/relationship signal where one exists (kept visibly separate
from the objective score), and packaging the result as an executive summary, market landscape,
per-vendor deep dives, and a strategic recommendation — for a deck or a standalone report.

Generalized from a 2026-05 four-vendor "AEV" (Adversarial Exposure Validation) market scan built for
a senior stakeholder, and the lightweight six-week "market update" that followed it. This skill
captures the methodology, not that scan's actual vendor ratings — those are internal competitive
intelligence and aren't reproduced here.

## Requirements

- None, strictly — the core workflow (rubric design, evidence gathering via `WebSearch`, per-vendor
  subagents, QA) works with only the tools every Claude Code session already has.
- (Optional, additive) A Salesforce CRM connector (or equivalent, exposing SOQL/SOSL query tools) to
  pull an internal pipeline-signal overlay for any focal vendor that's already a partner. The skill
  discovers the connector's tool names dynamically via `ToolSearch` and skips this section entirely
  for vendors with no internal relationship.
- (Optional) An internal page-hosting service (e.g. WWT's `my-pages`) to publish an HTML version of
  the scan to a shareable URL. Without one, write the report to a local file, or hand off the content
  for a deck (PowerPoint/Gamma) instead — see Workflow step 8 in `SKILL.md`.

## Install

```
/plugin marketplace add MartinGNystrom/market-scan
/plugin install wwt-market-scan@wwt-market-scan
```

## Usage

Ask Claude something like:

> Build a market scan comparing these four EDR vendors on autonomy, detection depth, and
> deployment friction: Acme, Widget Security, Contoso Defend, Fabrikam Shield.

The skill will:

1. Scope the category, the focal vendor set, and the decision the scan is meant to inform
2. Build a fixed feature rubric (5-8 capability categories, a shared rating scale) and tag every
   rating with a confidence level tied to evidence quality, not favorability
3. Launch one subagent per focal vendor (4+) to score the rubric with citations, write a company
   narrative, and pull an internal pipeline-signal overlay if one exists
4. Run a QA subagent to check the rubric was applied consistently, recompute every rollup, and
   flag any Low-confidence rating stated as settled fact
5. Package an executive summary, market landscape, per-vendor deep dives, a strategic
   recommendation, and a named next step — as a deck outline or a standalone report

See `skills/market-scan/SKILL.md` for the full workflow and
`skills/market-scan/references/fork-prompt-templates.md` for the exact subagent prompts used.

## Notes

- Read-only everywhere it touches a live system (CRM, web search) — nothing is written or posted
  anywhere as part of building the scan.
- The rubric's actual categories and features are specific to the technology being scanned — this
  skill teaches the *pattern* (fixed scale, confidence tagging, separated internal-signal overlay,
  consistency-checked QA), not a canned checklist to reuse verbatim across unrelated categories.

## License

MIT — see `LICENSE`.
