# ResForge

An open-source prompt engineering system that produces JD-specific, evidence-bound resumes and cover letters. Four modules, 929 rules, eight quality gates. Runs in Claude (claude.ai). No code required.

## What This Is

ResForge is a four-module prompt engineering system. You paste it into an AI chat (Claude recommended), provide your resume and a job description, answer targeted questions about your experience, and it produces an optimized resume where every claim traces to evidence you confirmed.

If the system cannot honestly align your experience with the job requirements, it returns a NO-GO verdict and recommends you apply elsewhere.

## How It Works

**Module 1 (JD Ingestion)** analyzes the job description, classifies requirements by priority, and generates 20+ targeted questions to surface evidence from your experience. Produces an Evidence Ledger of confirmed facts.

**Module 2 (D1 Drafting)** drafts an optimized resume and runs eight quality gates: word count enforcement, banned phrase detection, verb deduplication, evidence integrity, keyword placement, sentence flow analysis, metric-context verification, and summary quality checks.

**Module 3 (D2 Generation)** checks whether top bullets can be improved with unused evidence, compresses Independent Projects into a scannable format, and produces the final clean resume.

**Module 4 (Cover Letter)** creates a cover letter with real-time company research and seven verification gates, plus structured interview stories, red flag response scripts, and questions to ask the interviewer.

**What if I have skill gaps?** If Module 1 identifies skill-based gaps you want to address before applying, the portfolio/ folder contains a companion prompt that prescribes targeted projects, provides execution plans, and generates resume-ready bullets for completed work. This is optional.

## Quick Start

1. Create a Claude account at claude.ai (free tier works, Pro recommended)
2. Open a new chat
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

**Gate architecture:** Eight quality gates with blocking/advisory distinction. Blocking gates halt output until violations are resolved.

**No-fabrication enforcement:** Bans overclaiming, defensive framing, and AI-pattern language. If evidence is insufficient, returns NO-GO.

**Checkpoint system:** Mandatory stops prevent AI context window exhaustion. Each module has 1-4 checkpoints.

## Known Limitations

84.7% of rules depend on model attention (guardrail enforcement) rather than code verification. Banned phrases slip through at approximately 10-20% rate. Summary openings tend toward template language. Cover letter sentence rhythm can be monotone on Sonnet. The system was primarily tuned for career-change applications from government/international organizations to private sector; other career paths will encounter failure modes not yet addressed.

These are documented limitations, not hidden ones. Contributions that address them are welcome.

## Contributing

See CONTRIBUTING.md for guidelines. Every proposed change goes through a nine-criteria self-audit. The system reached 929 rules by finding failures and fixing them one at a time.

## License

MIT License. See LICENSE file.
<img width="468" height="639" alt="image" src="https://github.com/user-attachments/assets/a2c7fbc9-f6f9-4d7c-93d6-083f29e96494" />
