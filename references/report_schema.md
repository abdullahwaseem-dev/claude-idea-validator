# Report JSON Schema

This is the exact structure `scripts/generate_report.py` expects. Fields marked *(optional)* may be omitted entirely; every other field should be filled with real, research-backed content.

```jsonc
{
  "meta": {
    "idea_title": "string — short name for the idea",
    "one_line_pitch": "string — the idea in one sentence, as the user described it (plus your restated assumptions if you had to fill gaps)",
    "date": "string — e.g. 2026-09-11",
    "verdict": "VALIDATED | CONDITIONAL | PIVOT",
    "verdict_headline": "string — one sentence summarizing the verdict and the single biggest reason for it"
  },
  "executive_summary": "string — 2-4 short paragraphs, separated by \\n\\n",
  "market_landscape": {
    "overview": "string — what this market is and how it's currently structured",
    "market_size_estimate": "string — sized with hedge language and a source note, e.g. 'Estimated $X-Y range based on [source], as of [date]'",
    "growth_trends": ["string", "..."],
    "demand_signals": ["string", "..."],
    "data_confidence": "high | medium | low",
    "data_limitations": "string (optional, required if data_confidence is 'low') — what couldn't be found and why the estimate above is a proxy"
  },
  "competitors": [
    {
      "name": "string",
      "type": "direct | indirect | substitute",
      "description": "string",
      "strengths": ["string", "..."],
      "weaknesses": ["string", "..."],
      "pricing_positioning": "string"
    }
  ],
  "target_audience": {
    "primary_segment": "string",
    "secondary_segments": ["string", "..."],           // optional
    "pain_points": ["string", "..."],
    "willingness_to_pay": "string",
    "acquisition_channels": ["string", "..."]
  },
  "viability_scores": {
    "market_size": { "score": 1, "rationale": "string" },
    "competition_intensity": { "score": 1, "rationale": "string" },
    "differentiation": { "score": 1, "rationale": "string" },
    "feasibility": { "score": 1, "rationale": "string" },
    "timing": { "score": 1, "rationale": "string" },
    "monetization": { "score": 1, "rationale": "string" },
    "composite": 3.4,
    "composite_band": "VALIDATED | CONDITIONAL | PIVOT"
  },
  "opportunities": ["string", "..."],
  "risks": ["string", "..."],
  "recommendation": {
    "verdict": "VALIDATED | CONDITIONAL | PIVOT",
    "rationale": "string — the core argument for this verdict",
    "suggested_refinements": ["string", "..."],        // optional — for VALIDATED/CONDITIONAL
    "alternatives": [                                   // required if verdict == PIVOT, 1-3 items
      {
        "name": "string",
        "pitch": "string — one-line description",
        "why_better": "string — why this beats the original idea specifically",
        "evidence": "string — the research finding this is grounded in"
      }
    ]
  },
  "sources": [
    { "label": "string — publication/site name and short description", "url": "https://..." }
  ]
}
```

## Notes for filling this in

- `viability_scores.composite` and `composite_band`: compute using the formula in `references/scoring_rubric.md`. Don't let the script guess — supply the computed values directly so the report and your stated verdict always agree.
- `sources`: include every source a specific number or named-competitor claim in the report traces back to. Aim for at least 5–8 for a normal report.
- Keep list items concise (one sentence each) — the generator renders them as bullets, not paragraphs.
- A minimal but complete example lives at the bottom of this file for reference structure only (not real research).

<details>
<summary>Minimal example instance</summary>

```json
{
  "meta": {
    "idea_title": "Async Standup Bot for Slack",
    "one_line_pitch": "A Slack bot that collects async daily standups and summarizes blockers for engineering managers.",
    "date": "2026-09-11",
    "verdict": "CONDITIONAL",
    "verdict_headline": "The core mechanic is sound but the general market is crowded; a narrow vertical focus is the better bet."
  },
  "executive_summary": "The async-standup category is mature and dominated by well-funded incumbents (Geekbot, Standuply, Range) with similar feature sets.\n\nThe strongest opening is not the general engineering-team market but a narrower vertical those incumbents haven't targeted with purpose-built workflows.",
  "market_landscape": {
    "overview": "Async standup tools are an established Slack/Teams app category, typically sold as a per-seat add-on to existing chat tools.",
    "market_size_estimate": "No independent sizing found for this specific sub-category; proxy is the broader team-collaboration-software market, which multiple analyst reports place in the tens of billions and growing.",
    "growth_trends": ["Continued shift to hybrid/remote engineering teams sustains demand for async check-ins."],
    "demand_signals": ["Active discussion threads in r/ExperiencedDevs and r/engineeringmanagers about standup fatigue and tool switching."],
    "data_confidence": "medium",
    "data_limitations": "Category-specific revenue/user figures for standup bots specifically are not publicly reported; sizing above uses the broader collaboration-tools market as a proxy."
  },
  "competitors": [
    {
      "name": "Geekbot",
      "type": "direct",
      "description": "Long-standing Slack-native async standup bot.",
      "strengths": ["Deep Slack integration", "Established brand in the category"],
      "weaknesses": ["Generic reporting, not tailored to any single vertical"],
      "pricing_positioning": "Per-active-user monthly pricing, positioned as a low-cost add-on."
    }
  ],
  "target_audience": {
    "primary_segment": "Engineering managers at 20-200 person software companies",
    "pain_points": ["Standup fatigue in distributed teams", "Blockers surfacing too late"],
    "willingness_to_pay": "Comparable tools charge low per-seat monthly fees, suggesting modest but real willingness to pay.",
    "acquisition_channels": ["Slack App Directory", "Engineering-management newsletters"]
  },
  "viability_scores": {
    "market_size": { "score": 3, "rationale": "Real but modest category with no independent sizing data." },
    "competition_intensity": { "score": 2, "rationale": "Several established, well-reviewed direct competitors." },
    "differentiation": { "score": 2, "rationale": "Feature set closely mirrors existing tools without a vertical wedge." },
    "feasibility": { "score": 5, "rationale": "A Slack bot with this scope is buildable by a small team quickly." },
    "timing": { "score": 3, "rationale": "No new unlock; remote-work tailwind is already mature, not new." },
    "monetization": { "score": 3, "rationale": "Comparable per-seat pricing model is proven in this category." },
    "composite": 2.9,
    "composite_band": "CONDITIONAL"
  },
  "opportunities": ["A vertical-specific version (e.g. for on-call/incident-heavy teams) has no dedicated incumbent."],
  "risks": ["Feature parity with Geekbot/Standuply is easy for them to replicate if this gains traction."],
  "recommendation": {
    "verdict": "CONDITIONAL",
    "rationale": "The general-purpose version is a weak bet against entrenched competitors, but narrowing to a specific vertical workflow addresses the differentiation gap directly.",
    "suggested_refinements": ["Scope v1 to a single vertical (e.g. on-call engineering teams) instead of general standups."],
    "alternatives": []
  },
  "sources": [
    { "label": "Geekbot pricing page", "url": "https://geekbot.com/pricing" }
  ]
}
```

</details>
