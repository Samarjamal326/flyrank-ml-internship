# FL-01: AI Workflow Audit and Tool Setup

**Student Profile**: B.Tech AI & ML Engineering Student  
**Track**: Applied Search Intelligence & Machine Learning  

---

## 1. AI Workflow Audit

The table below audits 15 recurring tasks across academic learning, machine learning engineering, and career development. Tasks are categorized into four operational modes: **Just Me**, **Collaborate with AI**, **Delegate to AI with Review**, and **Fully Automate**.

| # | Task | Frequency | Classification | One-line Rationale |
|---|---|---|---|---|
| 1 | Solving LeetCode & DSA Problems | Daily | Just Me | Problem-solving intuition and algorithmic reasoning under timed conditions must be developed unassisted for technical interviews. |
| 2 | Live Technical Coding Interviews | Weekly | Just Me | Real-time evaluations require unassisted personal reasoning, spontaneous communication, and independent coding under pressure. |
| 3 | Reading ML Research Papers | Weekly | Collaborate with AI | AI accelerates comprehension by summarizing complex mathematical proofs and architectural trade-offs, while I synthesize core insights. |
| 4 | Machine Learning Model Development | Weekly | Collaborate with AI | AI assists in brainstorming feature engineering strategies and model selection, while I design the leak-free validation framework. |
| 5 | Building Full-Stack Web Applications | Weekly | Collaborate with AI | AI acts as a pair programmer for UI components and boilerplate endpoints, allowing me to focus on system architecture and state management. |
| 6 | Learning New AI Frameworks & Libraries | Weekly | Collaborate with AI | AI provides interactive code explanations and minimal reproducible examples for new tools (e.g. PyTorch Lightning, DuckDB, LangChain). |
| 7 | Planning Final-Year Capstone Project | Bi-weekly | Collaborate with AI | AI helps evaluate project feasibility, architectural choices, and literature gaps while I define business objectives and scope. |
| 8 | Debugging Python & ML Code | Daily | Delegate to AI with Review | AI rapidly identifies syntax errors, shape mismatches, and stack traces, which I verify before applying to the codebase. |
| 9 | Writing Technical Documentation & Readmes | Weekly | Delegate to AI with Review | AI drafts initial API documentation and setup guides from raw code snippets, which I review for accuracy and technical precision. |
| 10 | Writing ML Research Notes & Summaries | Weekly | Delegate to AI with Review | AI organizes rough experimental notes into structured Markdown summaries, which I verify against experimental logs. |
| 11 | Hackathon Project Scaffolding | Monthly | Delegate to AI with Review | AI generates initial project boilerplate, API integrations, and styling templates under tight deadlines, subject to code review. |
| 12 | Resume & Portfolio Optimization | Monthly | Delegate to AI with Review | AI tailors resume bullet points to highlight impact and technical keywords, which I verify against actual project contributions. |
| 13 | LinkedIn Technical Content Creation | Bi-weekly | Delegate to AI with Review | AI outlines post drafts and formatting based on my technical project milestones, which I refine to ensure authenticity. |
| 14 | GitHub Project Management & Issues | Weekly | Fully Automate | Automated scripts generate release notes, format PR templates, and triage issue labels without manual intervention. |
| 15 | Internship Application Tracking | Weekly | Fully Automate | Automated scripts log submission dates, status updates, and company metadata directly into a tracking dashboard. |

---

## 2. Three Target Tasks

The three tasks selected for maximum AI enhancement over the next 8 weeks are:

### Target Task 1: Debugging Python & ML Pipeline Code
- **Why it matters**: Debugging tensor shape mismatches, CUDA out-of-memory errors, data leakage, and pandas transformation bugs accounts for up to 40% of development time. Accelerating root-cause diagnosis keeps project momentum high.
- **Success Definition**: Using AI as a diagnostic assistant to explain error tracebacks and suggest localized fixes without swallowing exceptions or compromising code design.
- **Measurable Completion Criteria**:
  - *Time Saved*: Reduce mean-time-to-resolution (MTTR) for complex Python/ML bugs from 45 minutes to < 10 minutes (75%+ time reduction).
  - *Accuracy & Quality*: 90%+ first-pass fix resolution rate without introducing secondary regressions.
  - *Production-Ready Output*: Zero suppressed exceptions or silent fallback code introduced during debugging.

### Target Task 2: Machine Learning Model Development & Feature Engineering
- **Why it matters**: Building end-to-end ML models requires rapid iteration over feature transformations, model architectures, and validation splits. AI pair programming enables testing multiple hypotheses efficiently.
- **Success Definition**: Systematically evaluating alternative model architectures (e.g., decision trees vs. ensemble methods) and feature interactions while maintaining strict client-holdout validation discipline.
- **Measurable Completion Criteria**:
  - *Fewer Revisions*: Decrease model iteration cycles by 50% through AI-guided baseline selection and feature auditing.
  - *Production-Ready Output*: 100% adherence to leak-free feature pipelines and reproducible evaluation scripts (`scripts/01`–`05`).
  - *Independent Understanding*: Ability to articulate model trade-offs and feature importance scores in technical reports.

### Target Task 3: Reading & Summarizing ML Research Papers
- **Why it matters**: Staying current with state-of-the-art search intelligence, ranking models, and LLM architectures requires parsing dense academic literature efficiently.
- **Success Definition**: Extracting core mathematical formulations, dataset assumptions, and architectural innovations from papers in under 15 minutes per paper.
- **Measurable Completion Criteria**:
  - *Time Saved*: Cut paper analysis time from 2 hours to 25 minutes per paper (80% time reduction).
  - *Independent Understanding*: High-fidelity technical synthesis enabling immediate implementation of key algorithms in PyTorch/Python.
  - *Output Quality*: Creation of structured Markdown research summaries containing zero hallucinated claims or overstatements.

---

## 3. Claude Project Custom Instructions

Copy and paste the text block below into your Claude Project custom instructions:

```text
You are acting as an expert AI/ML engineering mentor, technical code reviewer, and tutor for a B.Tech Computer Science student specializing in Artificial Intelligence & Machine Learning. 

Key Guidelines & Profile Constraints:
1. Primary Focus: Machine Learning, Deep Learning, Search Intelligence, and Full-Stack Engineering (Python, PyTorch, pandas, scikit-learn, TypeScript/React).
2. Pedagogical Style: Always prioritize first-principles explanations, intuition, and architectural trade-offs BEFORE providing code solutions. Ask guiding questions to reinforce independent learning.
3. Response Tone: Concise, technically rigorous, precise, and professional. Avoid fluff, unnecessary conversational filler, or overly generic summaries.
4. Coding Standards: Write clean, modular, production-ready Python code adhering to PEP8. Include docstrings, explicit type hints, and robust error handling. Never introduce silent fallback values or swallow exceptions.
5. Algorithmic Thinking: When reviewing algorithms or DSA problems, analyze time/space complexity (Big-O) explicitly and guide optimization step-by-step.
6. Research & Claims Discipline: Enforce strict scientific discipline. Distinguish clearly between correlation vs causality, observational findings vs experimental proof, and leak-free validation vs proxy shortcuts.
```

---

## 4. Manual Steps Remaining

Complete the following external setup steps to finalize your AI tool environment:

- [ ] Create Claude account at [claude.ai](https://claude.ai)
- [ ] Create Anthropic Academy account at [academy.anthropic.com](https://academy.anthropic.com)
- [ ] Enroll in **AI Fluency: Framework & Foundations** course
- [ ] Complete Module 1 of AI Fluency framework
- [ ] Create a new Claude Project titled `FlyRank ML Internship`
- [ ] Copy and paste the provided custom instructions into the Claude Project instructions field
- [ ] Take a screenshot of the configured Claude Project interface
- [ ] Take a screenshot of the Anthropic Academy course enrollment confirmation page

---

## 5. Assignment Rubric Self-Check

| Criteria | Status | Verification Detail |
|---|---|---|
| At least 10 tasks in audit table | PASS | Includes 15 distinct recurring academic and engineering tasks. |
| Every task classified correctly | PASS | Uses strictly allowed categories (`Just Me`, `Collaborate with AI`, `Delegate to AI with Review`, `Fully Automate`). |
| Every task has one-line rationale | PASS | 100% of tasks include concise, realistic one-line justifications. |
| At least two "Just Me" tasks | PASS | 2 tasks explicitly designated `Just Me` (LeetCode/DSA & Live Technical Interviews). |
| Three target tasks defined | PASS | Detailed breakdown for Debugging, Model Development, and Paper Reading. |
| Measurable completion criteria | PASS | Explicit metrics included (time saved, accuracy, fewer revisions, independent understanding). |
| Custom instructions provided | PASS | Complete prompt tailored for B.Tech AI & ML student profile. |
| Manual steps checklist present | PASS | Un-fabricated checklist provided for external accounts & screenshots. |
