---
name: wsq-assessment
description: Generate or revise the WSQ assessments for THIS course (Microsoft Copilot Studio & Power Automate for Business Workflow Automation). Produces a Written Assessment (WA) and a Case Study (CS) Assessment, each as a question paper plus a model-answer / marking guide DOCX. ALL questions are OPEN-ENDED — no multiple choice. The Written Assessment is open-ended short-answer testing knowledge from Modules 1–4 and the slides; the Case Study is one coherent ACME Pte Ltd scenario whose model answers mirror the hands-on lab build steps (Labs 1–16). Use when editing the assessment questions, answers, case study, or marking guides for this course.
---

# WSQ Assessment — this course

Single-source generator: `courseware/build_assessment.py`. Outputs four DOCX into `assessemnt/`:
- `Written Assessment(WA) - <course>.docx` + `Answers to Written Assessment(WA) - <course>.docx`
- `Case Study(CS) Assessment - <course>.docx` + `Answers to Case Study(CS) Assessment - <course>.docx`

## Hard rules (do not break)
- **NO multiple choice — every question is OPEN-ENDED.** The Written Assessment uses open-ended short-answer questions with ruled answer lines.
- **Written (WA) = KNOWLEDGE** drawn from the concept modules and slides. Source list: `labs/Day 1/Module 1`, `Module 2`, `labs/Day 2/Module 3`, `labs/Day 3/Module 4`, and `courseware/facilitator-slides.pptx`. Each answer-key item cites its module/slide.
- **Case Study (CS) = PRACTICAL.** One coherent **ACME Pte Ltd** scenario built from the in-class activities; the **model answers are the lab build steps** (cite the labs in `labs/`).
- Keep questions and answers strictly to content taught in the modules, slides, and labs.

## How to edit
1. Edit the content lists in `courseware/build_assessment.py`:
   - `WRITTEN` — open-ended knowledge Q&A `(question, answer_lines, source, [model points])`.
   - `SCENARIO* / CS_Q / CS_A` — the ACME case study, the four practical tasks (A1–A4), and the lab-step model answers.
2. Run: `python3 courseware/build_assessment.py`
3. Verify: zero MCQ, every CS answer cites a lab, the four files regenerate in `assessemnt/`.

## Notes
- Keep `assessemnt/` free of other courses' files.
- Criterion tags: Written → `K1…`; Case Study practical → `A1…` (same numbering in paper and answer key).
- See the user-level `wsq-assessment` skill for the reusable, course-agnostic template.
