# Viability Scoring Rubric

Score each dimension 1–5 using the anchors below. Every score needs a one-sentence rationale tied to something found during research — not a gut feel.

## 1. Market Size & Growth (weight ×1.0)
| Score | Anchor |
|---|---|
| 1 | Vanishingly small or shrinking market; no credible path to a sustainable business. |
| 2 | Small niche, flat or declining; would require an unrealistic share to matter. |
| 3 | Moderate, stable market; a real but modest business is plausible. |
| 4 | Sizeable and growing market with clear tailwinds. |
| 5 | Large and/or fast-growing market with strong structural tailwinds (regulatory, technological, demographic). |

## 2. Competition Intensity (weight ×0.8, inverted — high competition without differentiation scores low)
| Score | Anchor |
|---|---|
| 1 | Saturated with entrenched, well-funded incumbents and strong network effects; no realistic wedge. |
| 2 | Several capable competitors already serve this need well. |
| 3 | Competitors exist but have clear, exploitable gaps (pricing, UX, segment neglect). |
| 4 | Few direct competitors; mostly indirect/substitute solutions. |
| 5 | Little to no real competition, and the gap isn't empty because the market is illusory. |

## 3. Differentiation / Moat (weight ×1.0)
| Score | Anchor |
|---|---|
| 1 | No meaningful difference from existing options; easily copied. |
| 2 | Minor differentiation (UI polish, price) that competitors could replicate quickly. |
| 3 | Meaningful differentiation (workflow, niche focus, data, integration) with some defensibility. |
| 4 | Strong differentiation with a plausible moat (proprietary data/workflow lock-in, network effects, unique access). |
| 5 | Hard-to-replicate advantage with compounding returns (data flywheel, strong network effects, regulatory/licensing moat). |

## 4. Execution Feasibility (weight ×0.8)
| Score | Anchor |
|---|---|
| 1 | Requires resources, licenses, or technology far beyond what's remotely realistic for the stated builder. |
| 2 | Very heavy lift (regulated, capital-intensive, deep-tech) relative to typical resources. |
| 3 | Buildable but non-trivial; needs real time, skill, or capital. |
| 4 | Achievable by a small, competent team in a reasonable timeframe. |
| 5 | A focused individual or small team could ship a credible version quickly. |

## 5. Timing (weight ×0.7)
| Score | Anchor |
|---|---|
| 1 | Clearly too early (no enabling technology/behavior yet) or too late (window has closed, incumbents entrenched). |
| 2 | Timing is questionable in one direction. |
| 3 | Timing is neutral — no strong tailwind or headwind either way. |
| 4 | Good timing — an enabling shift (tech, regulation, behavior) is underway. |
| 5 | Excellent timing — a clear, recent unlock (platform change, regulation, cost collapse, behavior shift) directly benefits this idea now. |

## 6. Monetization Potential (weight ×0.9)
| Score | Anchor |
|---|---|
| 1 | No credible path to revenue, or target users demonstrably won't pay. |
| 2 | Weak willingness to pay; comparable products struggle to monetize. |
| 3 | Plausible monetization, comparable to how similar products charge. |
| 4 | Clear monetization path with evidence of willingness to pay (comparable pricing, existing spend on alternatives). |
| 5 | Strong, proven monetization model directly evidenced by comparable products' pricing/revenue. |

## Composite score

```
composite = (market_size×1.0 + competition_intensity×0.8 + differentiation×1.0
             + feasibility×0.8 + timing×0.7 + monetization×0.9) / 4.2
```

This normalizes back to a 1–5 scale.

| Composite | Band |
|---|---|
| ≥ 3.8 | VALIDATED |
| 2.8 – 3.79 | CONDITIONAL |
| < 2.8 | PIVOT |

## Fatal-flaw overrides

Any of these forces a **PIVOT** recommendation regardless of composite score:

- A dominant free or open-source incumbent with strong network effects and no viable wedge around it.
- Unit economics that cannot work at any realistic scale (cost per user/transaction structurally exceeds realistic willingness to pay).
- A hard regulatory or legal dead-end for the stated business model in its stated market.
- The idea depends on a two-sided marketplace with no credible cold-start plan and no unique supply- or demand-side wedge.
- The core assumption about user behavior is directly contradicted by evidence found during research (e.g., target users are shown to actively avoid paying for this category).

When a fatal flaw applies, state it explicitly and explain why it overrides the composite score before presenting alternatives.
