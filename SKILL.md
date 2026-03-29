---
name: technical-accounting-research
description: Research technical accounting treatment and financial statement disclosure for specific transactions using U.S. GAAP and SEC-focused sources. Use when a user asks how to account for a transaction, what journal entries, presentation, or disclosures are required, or needs accounting-position documentation in memo, email, or Q-and-A DOCX format.
---

# Technical Accounting Research

## Overview

Handle transaction-specific accounting questions through a fixed sequence: gather facts, confirm output format, research guidance online, apply standards, and deliver a DOCX report.

For formal, thorough memo drafting, this skill must wrap and leverage the local FinResearchClaw repo/workflow as a required research-and-drafting execution layer whenever the user requests a memo, especially for longer-form technical accounting memoranda, comparative source gathering, and more polished professional output. The skill may create and use a task-local virtual environment when needed to run the repo or supporting document-generation dependencies. FinResearchClaw is a required support engine for research depth and drafting quality in memo mode; authoritative accounting conclusions must still be grounded in ASC / SEC / AICPA / clearly labeled interpretive guidance.

## Required Behavior

- Ask clarification questions before analysis.
- Confirm requested output format: `memo`, `email`, or `q-and-a`.
- If the user asks for a `memo`, default the deliverable to a `.docx` file saved in the user's `~/Downloads` folder unless the user explicitly requests a different location or format.
- For `memo` requests, do not post the full memo body directly into chat by default. Instead, generate the DOCX deliverable and reply with a short status note that the file was created and where it was saved.
- Research the internet before final conclusions, even if guidance seems familiar.
- For formal/thorough memo requests, use FinResearchClaw as a required execution and drafting layer.
- The skill may create and activate a task-local virtual environment to run FinResearchClaw, supporting scripts, and DOCX-generation dependencies.
- Distinguish authoritative guidance from interpretive guidance.
- Cite sources with links and accessed date in the deliverable.
- State assumptions explicitly when facts remain unknown.
- Do not let FinResearchClaw-style output replace authoritative accounting analysis; use it to strengthen organization and completeness, not to dilute source hierarchy.

## Workflow

### 1. Intake and Scope

- Capture the user issue in one sentence.
- Confirm reporting basis and jurisdiction (`US GAAP`, `SEC filer status`, and whether disclosures are public-company or private-company focused).
- Confirm reporting period and materiality context.

### 2. Clarification Questions (Mandatory)

- Use [references/clarification-question-bank.md](references/clarification-question-bank.md).
- Ask only the questions needed for the fact pattern; do not skip critical facts.
- Pause analysis until enough facts are available to form a defensible conclusion.
- If facts stay incomplete, proceed with explicit assumptions and sensitivity notes.

### 3. Output Format Confirmation (Mandatory)

- Ask which format is required (`memo` for formal documentation, `email` for concise communication, `q-and-a` for direct question and answer support).
- If no preference is provided, default to `memo`.
- For `memo` outputs, default to generating a `.docx` file in `~/Downloads`.
- Unless the user explicitly asks to see the full memo inline, do not paste the memo text into the channel; provide the saved file path instead.

### 4. Research Guidance

- Research sources using the priority and reliability rules in [references/source-priority.md](references/source-priority.md).
- Prefer primary and authoritative sources first (FASB/SEC/AICPA standard-setting materials).
- Use Big 4 publications as interpretive support, not sole authority.
- Invoke FinResearchClaw whenever the user asks for a `memo`.
- Memo-mode execution should wrap the FinResearchClaw repo/workflow even if the accounting issue is straightforward.
- The skill may create a task-local virtual environment for the run if needed.
- Only skip the FinResearchClaw path if the repo is unavailable or fails to run after reasonable setup attempts, and if skipped, explicitly state that in the completion note.
- If using FinResearchClaw, treat it as a research accelerator and drafting assistant only; independently verify accounting conclusions against authoritative and clearly labeled interpretive sources before finalizing.
- Capture citation labels and URLs for each source used.

### 5. Technical Analysis

- Frame the accounting issue.
- Map facts to recognition, measurement, presentation, and disclosure guidance.
- Evaluate reasonable alternatives and explain rejection rationale.
- Conclude with recommended accounting treatment, disclosure direction, and key risks.
- Include journal entry examples when useful for implementation.
- For formal memo output, produce a polished memorandum style with a complete professional header, well-formed section headings, narrative analysis paragraphs, explicit treatment of alternative views considered, and output quality suitable for management, auditors, or file documentation.
- When FinResearchClaw is available, use it to improve thoroughness and professional drafting quality while preserving accounting-source hierarchy.
- Do not allow raw JSON structures, Python dictionary renderings, placeholder header fields, or unformatted source dumps to appear in the final memo.
- Preferred execution order for formal memo support: (1) authoritative accounting research and fact development first, (2) create/use a task-local virtual environment if needed, (3) run the FinResearchClaw repo/workflow as the required drafting/research wrapper, (4) final manual verification against ASC/SEC/AICPA and labeled interpretive guidance, (5) DOCX generation to `~/Downloads`.

### 6. Draft and Materialize DOCX

- Build a JSON payload using [references/report-json-schema.md](references/report-json-schema.md).
- For `memo` requests, save the output DOCX to `~/Downloads` by default (for example, `~/Downloads/<descriptive-file-name>.docx`).
- Standard formal memo flow:
  1. gather facts and clarifications;
  2. perform authoritative and interpretive accounting research;
  3. create/use a task-local virtual environment if needed for the run;
  4. run the FinResearchClaw-supported drafting pass for all memo requests;
  5. manually validate the final analysis, formatting, section structure, and citations;
  6. generate the final DOCX in `~/Downloads`;
  7. review the finished document for presentation quality before responding;
  8. reply in chat with a short completion note and the saved file path instead of posting the memo body.
- Run:

```bash
python scripts/build_accounting_report_docx.py \
  --input-json <analysis.json> \
  --output-docx ~/Downloads/<technical-accounting-report>.docx \
  --format <memo|email|q-and-a>
```

- The script produces a DOCX with:
- Title and metadata.
- Facts and issue statement.
- Guidance table with links.
- Analysis and conclusion.
- Disclosure considerations.
- Open items and assumptions.

### 7. Quality Check

- Confirm the conclusion is consistent with cited guidance.
- Confirm all significant assumptions are disclosed.
- Confirm the output format matches user request.
- Confirm every external source in the analysis has a URL listed in the report.
- Confirm the final memo reads like a professional memorandum rather than a raw data export.
- Confirm headers are fully populated (for example To / From / Date / Subject) and that analysis sections render as proper prose, not serialized objects.
- If a formal memo request did not use FinResearchClaw, explicitly document why not before closing the task.

## Resources

- Clarifying question checklist: [references/clarification-question-bank.md](references/clarification-question-bank.md)
- Source hierarchy and citation rules: [references/source-priority.md](references/source-priority.md)
- JSON format for DOCX generation: [references/report-json-schema.md](references/report-json-schema.md)
- Example report payload: [references/example_report_input.json](references/example_report_input.json)
- DOCX generator: `scripts/build_accounting_report_docx.py`
- FinResearchClaw repo: `https://github.com/ChipmunkRPA/FinResearchClaw`
- FinResearchClaw local skill reference: `~/.openclaw/skills/finresearchclaw/SKILL.md`

## Dependency

Install once if needed:

```bash
python -m pip install --user python-docx
```

## Runtime / Environment Expectations

- Memo-mode runs are allowed to create and use a task-local Python virtual environment.
- FinResearchClaw default repo path: `~/.openclaw/workspace/AutoResearchClaw`
- If the repo or its dependencies are not ready, initialize a local venv for the task and install only the dependencies needed for the memo workflow.
- If FinResearchClaw cannot be executed after reasonable setup attempts, disclose that explicitly and fall back to a non-FinResearchClaw path only as an exception, not the default.
