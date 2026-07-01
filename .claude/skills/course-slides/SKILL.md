---
name: course-slides
description: Edit / update THIS course's facilitator slide deck (courseware/facilitator-slides.pptx, 94 slides, white theme, Arial) for "Microsoft Copilot Studio & Power Automate for Business Workflow Automation". There is NO slide build script — the deck is edited in place with python-pptx. Use when a slide is out of date (e.g. a Copilot Studio UI change), must match an updated lab, or needs a text/screenshot fix. Keeps the deck aligned with the Lesson Plan's Slides column and the Learner Guide.
---

# Facilitator slides — edit in place

The deck `courseware/facilitator-slides.pptx` has **no generator script**; edit it directly with `python-pptx`. Keep it aligned with the labs in `labs/`, the Learner Guide (`build_learner_guide.py`), and the Lesson Plan's **Slides** column (`build_lesson_plan.py`).

## Golden rule — edit at the RUN level (preserve formatting)
Never set `text_frame.text` or `paragraph.text` — that collapses runs and loses font/size/colour/bold. Set the text on the existing run and assert the old text first:

```python
from pptx import Presentation
p = Presentation("courseware/facilitator-slides.pptx")

def set_run(slide_idx, shape_idx, new_text, must_contain):   # 1-based slide index
    run = p.slides[slide_idx-1].shapes[shape_idx].text_frame.paragraphs[0].runs[0]
    assert must_contain in run.text, f"slide {slide_idx}: '{must_contain}' not found"
    run.text = new_text
    # ...
p.save("courseware/facilitator-slides.pptx")
```

A multi-line bullet block is usually a **single run** with `\n` separators — replace that one run to update the whole block while keeping its style.

## Find the slide/shape to edit
Print structure first: iterate `enumerate(p.slides, 1)` → `shape.has_text_frame` → `paragraphs` → `runs`, printing `run.text`. Match by visible title/text, not by guessing indexes.

## Rules for this deck
- **Do NOT add or delete slides.** The Lesson Plan maps sessions to slide numbers (e.g. Lab 9 → 55–56, 59; Module 3 → 40–49). Editing text in place keeps that mapping valid. If a slide must be added/removed, update the **Slides** column in `build_lesson_plan.py` and rebuild the LP + PDF in the same change.
- **White theme only, Arial, 16:9** — inherited automatically when you edit existing runs.
- Keep slide wording consistent with the labs. Current alignment done: slide 43 (topics are chosen by their **description** under generative orchestration) and slide 59 (Lab 9 = topic + Ask-a-question nodes, not a single prompt).

## Verify after editing
1. Re-read the changed slides' `run.text` to confirm.
2. (Optional) Export PDF: `soffice --headless --convert-to pdf --outdir courseware "courseware/facilitator-slides.pptx"`.

See the user-level `tertiary-course-slides` skill for the full house style and the from-scratch generator.
