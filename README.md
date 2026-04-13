# ResForge

An open-source prompt engineering system that produces JD-specific, evidence-bound resumes and cover letters. Four modules, 900+ rules, eight quality gates. Runs in Claude (claude.ai). No code required.

## What This Is

ResForge is a four-module prompt engineering system. You paste it into an AI chat (Claude recommended, Opus for best results), provide your resume and a job description, answer targeted questions about your experience, and it produces an optimized resume where every claim traces to evidence you confirmed.

If the system cannot honestly align your experience with the job requirements, it returns a NO-GO verdict and recommends you apply elsewhere.

## How It Works

**Module 1 (JD Ingestion)** analyzes the job description, classifies requirements by priority, and generates 20+ targeted questions to surface evidence from your experience. Produces an Evidence Ledger of confirmed facts with a Locked Metrics Table that locks the exact permissible phrasing for every metric before bullet drafting begins. Includes a Zero-MUST Fallback for JDs that classify all requirements as LIKELY_MUST.

**Module 2 (D1 Drafting)** drafts an optimized resume and runs eight quality gates: word count enforcement, banned phrase detection, verb deduplication, evidence integrity, keyword placement, sentence flow analysis, metric-context verification, and summary quality checks. Includes a Metric Promotion Ban that prohibits three specific fabrication patterns (observation-to-metric, reverse engineering, decomposition) and a Filler Bullet Detection check that flags padding bullets in the top two roles.

**Module 3 (D2 Generation)** checks whether top bullets can be improved with unused evidence, compresses Independent Projects with a JD-relevance check on lead bullets, runs an 11-dimension D2 Quality Scorecard that produces a concrete quality rating (9+, 8.5, 8, 7-7.5, or below 7), and outputs the final clean resume.

**Module 4 (Cover Letter)** creates a cover letter with real-time company research, a voice and conviction pre-check (CL-Gate 0) that tests whether the opening expresses a point of view or merely cites a company fact, and seven verification gates, plus structured interview stories, red flag response scripts, and questions to ask the interviewer.

**What if I have skill gaps?** If Module 1 identifies skill-based gaps you want to address before applying, the portfolio/ folder contains a companion prompt that prescribes targeted projects, provides execution plans, and generates resume-ready bullets for completed work. This is optional.

## Quick Start

1. Create a Claude account at claude.ai (free tier works, Pro recommended)
2. Open a new chat (Opus model recommended for best constraint adherence)
3. Copy the contents of Module_1_JD_Ingestion.docx from the modules/ folder
4. Paste it into the chat, followed by your resume and the job description
5. Follow the prompts — answer questions, type 'continue' at checkpoints
6. Repeat with Modules 2, 3, and 4 in the same chat

See guides/User_Guide.docx for detailed step-by-step instructions.

## Repository Structure

- **modules/** — The four core prompt files (paste these into Claude in order)
- **guides/** — User Guide and Q&A Archive setup instructions
- **templates/** — Blank Q&A Archive templates (Parts 1-3) for building your evidence base
- **portfolio/** — Optional companion prompt for building portfolio projects to address skill gaps

## Design Principles

**Evidence binding:** No claim appears on the resume without a confirmed source in the Evidence Ledger.

**Locked Metrics Table:** Every metric is locked with exact permissible phrasing before bullet drafting begins. Observational data is marked QUALITATIVE ONLY and cannot be promoted to quantified claims. Three specific fabrication patterns (observation-to-metric, reverse engineering, decomposition) are explicitly prohibited.

**Gate architecture:** Eight quality gates with blocking/advisory distinction. Blocking gates halt output until violations are resolved.

**No-fabrication enforcement:** Bans overclaiming, defensive framing, and AI-pattern language. If evidence is insufficient, returns NO-GO.

**D2 Quality Scorecard:** An 11-dimension final verification produces a concrete quality rating before output, covering evidence integrity, framing ladder accuracy, word counts, verb uniqueness, summary quality, filler detection, employment continuity, banned phrases, JD coverage, project relevance, and metric-context integrity.

**Checkpoint system:** Mandatory stops prevent AI context window exhaustion. Each module has 1-4 checkpoints.

## Model Recommendations

ResForge works with any Claude model but produces different quality levels:

**Opus (recommended for priority applications):** Best constraint adherence, most accurate self-scoring on the D2 Quality Scorecard. Self-scores within 0.5 points of external audit. Consistently avoids metadata leakage and framing ladder violations that Sonnet misses.

**Sonnet (acceptable for volume applications):** Faster and uses less of your message budget. Produces good structural quality but has a higher rate of banned phrase violations, filler bullets, and fabricated sub-counts. Self-scores can inflate by 1.5-2 points versus external audit. Best paired with manual metric verification before submission.

**Sonnet with Extended Thinking:** Improves structural quality (better JD coverage, fewer major metric fabrications) but does not reliably improve self-verification. The model uses the additional reasoning space to rationalize its choices rather than catch its own violations.

## Known Limitations

Most rules depend on model attention (guardrail enforcement) rather than code verification. Banned phrases slip through at approximately 5-15% on Opus, 10-20% on Sonnet. Summary openings tend toward template language ("Brings X to Y" pattern). Cover letter sentence rhythm can be monotone on Sonnet. The D2 Quality Scorecard reduces but does not eliminate self-assessment inflation — external verification is recommended for priority applications.

The system was primarily tuned for career-change applications from government/international organizations to private sector; other career paths will encounter failure modes not yet addressed.

These are documented limitations, not hidden ones. Contributions that address them are welcome.

## Contributing

See CONTRIBUTING.md for guidelines. Every proposed change goes through a nine-criteria self-audit. The system reached its current rule count by finding failures and fixing them one at a time.

## License

MIT License. See LICENSE file.
