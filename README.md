<div align="center">

# ResForge

**An open-source prompt engineering system that produces JD-specific, evidence-bound resumes and cover letters.**

Four modules &bull; 900+ rules &bull; Eight quality gates &bull; No code required

Runs entirely in [Claude](https://claude.ai) &mdash; just paste and follow the prompts.

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Compatible](https://img.shields.io/badge/Claude-Opus%20%7C%20Sonnet-blueviolet)](#model-recommendations)
[![No Code](https://img.shields.io/badge/Code%20Required-None-brightgreen)](#quick-start)

---

[What This Is](#what-this-is) &bull; [How It Works](#how-it-works) &bull; [Quick Start](#quick-start) &bull; [Repo Structure](#repository-structure) &bull; [Design Principles](#design-principles) &bull; [Model Recommendations](#model-recommendations) &bull; [Known Limitations](#known-limitations) &bull; [Contributing](#contributing)

</div>

## What This Is

ResForge is a four-module prompt engineering system. You paste it into an AI chat, provide your resume and a job description, answer targeted questions about your experience, and it produces an optimized resume where **every claim traces to evidence you confirmed**.

> **Honesty-first:** If the system cannot honestly align your experience with the job requirements, it returns a **NO-GO** verdict and recommends you apply elsewhere. It will not fabricate qualifications.

---

## How It Works

ResForge processes your application through four sequential modules, each building on the last:

```
  Resume + JD                Evidence                   Optimized              Cover Letter
       |                     Ledger                      Resume               + Interview Prep
       v                       v                           v                        v
 +-----------+          +------------+          +--------------+          +----------------+
 | Module 1  |  ------> |  Module 2  |  ------> |   Module 3   |  ------> |    Module 4    |
 |  Analyze  |          |   Draft    |          |   Optimize   |          |    Prepare     |
 +-----------+          +------------+          +--------------+          +----------------+
  JD Ingestion           D1 Drafting             D2 Generation            Cover Letter &
  + Gate 0               + 8 Quality Gates       + Quality Scorecard      Interview Prep
```

<details>
<summary><strong>Module 1 &mdash; JD Ingestion + Gate 0</strong></summary>

- Analyzes the job description and classifies requirements by priority
- Generates 20+ targeted questions to surface evidence from your experience
- Produces an **Evidence Ledger** of confirmed facts with a **Locked Metrics Table** that locks the exact permissible phrasing for every metric before bullet drafting begins
- Includes a Zero-MUST Fallback for JDs that classify all requirements as `LIKELY_MUST`
- Determines your Application Type: `CAREER_CHANGE`, `SAME_FIELD`, or `INTERNAL_TRANSFER`

</details>

<details>
<summary><strong>Module 2 &mdash; D1 Drafting</strong></summary>

- Drafts an optimized resume (D1) and runs **eight quality gates:**

  | Gate | What It Checks |
  |------|---------------|
  | Word Count | Bullet length enforcement per role tier |
  | Banned Phrases | AI-pattern language and overclaiming detection |
  | Verb Deduplication | No repeated action verbs across bullets |
  | Evidence Integrity | Every claim traces to the Evidence Ledger |
  | Keyword Placement | JD terminology appears in appropriate context |
  | Sentence Flow | Natural reading rhythm, no robotic patterns |
  | Metric-Context | Numbers match their confirmed source and context |
  | Summary Quality | Professional summary passes clarity checks |

- Includes a **Metric Promotion Ban** prohibiting three fabrication patterns: observation-to-metric, reverse engineering, and decomposition
- **Filler Bullet Detection** flags padding bullets in the top two roles
- You make decisions about Independent Projects (KEEP / REVISE / DROP)

</details>

<details>
<summary><strong>Module 3 &mdash; D2 Generation</strong></summary>

- Checks whether top bullets can be improved with unused evidence
- Compresses Independent Projects with a JD-relevance check on lead bullets
- Runs an **11-dimension D2 Quality Scorecard** producing a concrete rating:

  | Score | Meaning |
  |-------|---------|
  | **9+** | Exceptional &mdash; ready to submit |
  | **8.5** | Strong &mdash; minor polish possible |
  | **8** | Good &mdash; review flagged items |
  | **7&ndash;7.5** | Needs revision on specific dimensions |
  | **Below 7** | Significant issues &mdash; requires rework |

- Outputs your **final clean resume (D2)** and an ATS Confidence Score

</details>

<details>
<summary><strong>Module 4 &mdash; Cover Letter + Interview Prep</strong></summary>

- Creates a cover letter with real-time company research
- Runs **CL-Gate 0** (voice and conviction pre-check): tests whether the opening expresses a point of view or merely cites a company fact
- Seven verification gates ensure evidence-bound claims
- Produces:
  - **Interview Stories** &mdash; 3-4 structured stories with full and 30-second versions
  - **Red Flag Response Scripts** &mdash; pre-written responses for tough questions
  - **Questions to Ask** &mdash; based on company research
  - **Quick Reference Card** &mdash; one-page summary for pre-interview review

</details>

<details>
<summary><strong>Optional: Portfolio Development</strong></summary>

If Module 1 identifies skill-based gaps you want to address before applying, the `portfolio/` folder contains a companion prompt that prescribes targeted projects, provides execution plans, and generates resume-ready bullets for completed work.

</details>

---

## Quick Start

```
1. Create a Claude account       -->  claude.ai (free tier works, Pro recommended)
2. Open a new chat               -->  Opus model recommended for best results
3. Paste Module 1                -->  From modules/Module_1_JD_Ingestion.docx
4. Add your resume + job desc    -->  Paste text or upload files after the module text
5. Follow the prompts            -->  Answer questions, type 'continue' at checkpoints
6. Paste Modules 2, 3, 4        -->  In the same chat, one at a time
```

> **Important:** All four modules must run in the **same chat session**. Do not switch between chats mid-process.

See [`guides/User_Guide.docx`](resume-optimization-system:/guides:/ResForge_User_Guide.docx) for detailed step-by-step instructions.

---

## Repository Structure

```
ResForge/
  |-- modules/                  # The four core prompt files
  |     |-- Module_1_JD_Ingestion.docx
  |     |-- Module_2_D1_Drafting.docx
  |     |-- Module_3_D2_Generation.docx
  |     +-- Module_4_Cover_Letter.docx
  |
  |-- guides/                   # User Guide & Q&A Archive setup
  |     |-- ResForge_User_Guide.docx
  |     +-- QA_Archive_Instructions.docx
  |
  |-- templates/                # Blank Q&A Archive templates
  |     |-- QA_Archive_Template_1.docx
  |     |-- QA_Archive_Template_2.docx
  |     +-- QA_Archive_Template_3.docx
  |
  |-- portfolio/                # Optional skill-gap companion
  |     |-- Portfolio_Development_Prompt.docx
  |     +-- Portfolio_Instruction_Sheet.docx
  |
  |-- CONTRIBUTING.md
  +-- LICENSE (MIT)
```

---

## Design Principles

| Principle | What It Means |
|-----------|--------------|
| **Evidence Binding** | No claim appears on the resume without a confirmed source in the Evidence Ledger. |
| **Locked Metrics** | Every metric is locked with exact permissible phrasing before drafting. Observational data is marked `QUALITATIVE ONLY` and cannot be promoted to quantified claims. Three fabrication patterns are explicitly prohibited. |
| **Gate Architecture** | Eight quality gates with blocking/advisory distinction. Blocking gates halt output until violations are resolved. |
| **No-Fabrication Enforcement** | Bans overclaiming, defensive framing, and AI-pattern language. Insufficient evidence = NO-GO. |
| **D2 Quality Scorecard** | 11-dimension final verification produces a concrete quality rating before output. |
| **Checkpoint System** | Mandatory stops prevent AI context window exhaustion. Each module has 1&ndash;4 checkpoints. |

---

## Model Recommendations

| Model | Best For | Tradeoffs |
|-------|----------|-----------|
| **Opus** | Priority applications | Best constraint adherence. Self-scores within 0.5 pts of external audit. Catches metadata leakage and framing violations that Sonnet misses. |
| **Sonnet** | Volume applications | Faster, uses less message budget. Higher rate of banned phrase violations and filler bullets. Self-scores can inflate by 1.5&ndash;2 pts. Pair with manual metric verification. |
| **Sonnet + Extended Thinking** | Structural quality | Better JD coverage and fewer major metric fabrications, but does not reliably improve self-verification. Additional reasoning space tends to rationalize rather than catch violations. |

---

## Known Limitations

> These are documented limitations, not hidden ones. Contributions that address them are welcome.

- **Guardrail enforcement depends on model attention**, not code verification. Banned phrases slip through at ~5&ndash;15% on Opus, ~10&ndash;20% on Sonnet.
- **Summary openings** tend toward template language.
- **Cover letter rhythm** can be monotone on Sonnet (see the voice editing tip in the User Guide).
- **Self-assessment inflation** is reduced but not eliminated by the D2 Quality Scorecard &mdash; external verification is recommended for priority applications.
- **Career path tuning:** The system was primarily tuned for career-change applications from government/international organizations to private sector. Other career paths may encounter unaddressed failure modes.

---

## Contributing

Every proposed change goes through a **nine-criteria self-audit**. The system reached its current rule count by finding failures and fixing them one at a time.

See [CONTRIBUTING.md](CONTRIBUTING.md) for full guidelines.

---

## License

[MIT License](LICENSE)
