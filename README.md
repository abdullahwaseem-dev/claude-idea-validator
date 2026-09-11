# Idea Validator

**A Claude Skill that turns "I have an idea for..." into a researched, evidence-backed market analysis — with an honest verdict, not a pep talk.**

Ask ChatGPT or Claude to evaluate your startup idea and you usually get one of two useless answers: reflexive encouragement ("This could really work if you execute well!") or generic caution ("Consider your competition and target market carefully") — neither backed by anything you couldn't have guessed yourself. Meanwhile actual market research — competitor scans, demand-signal digging, TAM sizing, writing it all up — is exactly the kind of multi-step, source-heavy work that eats a weekend and that most people skip entirely before building.

**Idea Validator** closes that gap. Drop it into Claude, describe your idea, and it researches the space for real (competitors, pricing, demand signals, funding activity, timing), scores it against a fixed viability rubric, and hands you back a structured PDF and Word report — with a clear verdict: **validated**, **conditional**, or **pivot** (and if it's a pivot, 1–3 stronger alternative directions grounded in the same research, not just "no").

It won't tell you your idea is great to be nice. It won't tell you it's doomed for engagement either. It tells you what the market actually looks like and lets that speak.

---

## What you get

- **Real research, not guesses** — uses Claude's web search to pull current competitors, pricing, reviews, funding activity, and community demand signals before writing a word of analysis.
- **A fixed, transparent scoring rubric** — six weighted dimensions (market size, competition intensity, differentiation, feasibility, timing, monetization), each scored 1–5 with a cited rationale, rolled into one composite verdict. See [`references/scoring_rubric.md`](references/scoring_rubric.md).
- **Pivots grounded in evidence, not vibes** — when an idea is weak, it proposes alternatives sourced from gaps it actually found in the research (an underserved segment, a repeated complaint about incumbents, an open pricing tier) — not generic "have you considered..." filler.
- **Honest about data gaps** — for niche or obscure markets, it says so and shows its proxy reasoning instead of inventing a clean-looking statistic.
- **A real deliverable** — a formatted PDF and Word document you can open, edit, and send to a cofounder or investor, not just a wall of chat text.

## Installation

This is a [Claude Skill](https://www.anthropic.com/news/skills) — a folder Claude reads to gain a specific capability.

**Claude Code / CLI:**
```bash
git clone https://github.com/<your-username>/idea-validator.git
mkdir -p ~/.claude/skills
cp -r idea-validator ~/.claude/skills/
```
Restart Claude Code (or start a new session) and the skill is available automatically whenever you describe an idea.

**claude.ai (Claude with Skills enabled):**
1. Download this repo as a ZIP (or `git clone` it).
2. In Claude, go to **Settings → Capabilities → Skills** and upload the `idea-validator` folder.
3. Start a chat and describe your idea — Claude will invoke the skill on its own.

**Dependencies:** the report generator needs `reportlab` and `python-docx`. Claude installs them automatically the first time it runs the skill (`pip install -r requirements.txt`); if your environment blocks installs, do it once yourself:
```bash
pip install -r requirements.txt
```

## Usage

Just describe your idea in plain language:

> "I want to build a Chrome extension that automatically tracks how much time developers spend in each repo and shows a weekly report."

The skill will:
1. Ask a couple of clarifying questions if your idea is too thin to research (who it's for, how it makes money) — otherwise it goes straight to research.
2. Search for competitors, demand signals, pricing, and funding activity.
3. Score the idea against the viability rubric and decide: validate, validate-with-conditions, or pivot.
4. Generate `idea-name.pdf` and `idea-name.docx` in an `output/` folder and hand them to you.
5. Give you a short summary in chat — the verdict and the top evidence behind it — and point you to the full report for the rest.

### Example

**Input:**
> "Validate this idea: an app that lets small restaurants split delivery orders across DoorDash, Uber Eats, and Grubhub from one dashboard so they don't need three tablets."

**Chat response (abridged):**
> **Verdict: CONDITIONAL**
> The core pain point — restaurants juggling 3+ delivery tablets — is real and well-documented in restaurant-owner forums and trade press. But "unified order dashboard" is already a feature inside existing POS/aggregator tools (Otter, Deliverect) that have direct API deals with the delivery platforms, which is a hard integration moat for a new entrant to match.
>
> The better bet found in research: rather than competing head-on as a generic dashboard, target the segment those tools underserve — very small, single-location independent restaurants that current aggregator tools price and onboard for multi-location chains, not mom-and-pop shops.
>
> Full breakdown, competitor table, and scoring in the attached report.

**Files produced:**
- `output/delivery-order-dashboard.pdf`
- `output/delivery-order-dashboard.docx`

Each report contains: Executive Summary → Market Landscape → Competitor Analysis → Target Audience → Viability Scorecard → Opportunity & Risk Assessment → Recommendation (+ Alternatives if applicable) → Sources.

## How it works under the hood

- [`SKILL.md`](SKILL.md) — the full instruction set Claude follows: how to research, how to score, when to ask clarifying questions, when to recommend a pivot vs. validate, and how to hand off to the report generator.
- [`references/scoring_rubric.md`](references/scoring_rubric.md) — the six-dimension weighted viability rubric and the fatal-flaw overrides that force a pivot regardless of score.
- [`references/report_schema.md`](references/report_schema.md) — the exact JSON structure Claude fills in with research findings before generating documents.
- [`scripts/generate_report.py`](scripts/generate_report.py) — a standalone Python script (reportlab + python-docx) that turns that JSON into a formatted PDF and Word document. Works outside Claude too — feed it any JSON matching the schema.

This structure follows Anthropic's [Agent Skills](https://www.anthropic.com/news/skills) design: a lean `SKILL.md` with the core behavior, and reference/script files loaded only when needed — so it stays fast and cheap to invoke.

## Why this exists

Most "AI idea validator" tools are a single prompt wrapped in a SaaS landing page, charging for something a good prompt should do for free — and most of them skip the actual research step entirely, generating plausible-sounding analysis with no real sources behind it. This is the opposite bet: fully open, inspectable, and built to actually search before it opines. Fork it, tune the scoring weights to match how you evaluate ideas, swap in your own report branding — it's yours.

If it saved you from building the wrong thing, or helped you make the case for the right one, a star helps others find it.

## Contributing

Issues and PRs welcome — particularly around the scoring rubric (if you have a sharper way to weigh these dimensions), additional research angles, and report formatting improvements.

## License

[MIT](LICENSE)
