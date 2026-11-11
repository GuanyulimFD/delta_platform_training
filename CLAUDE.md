# deltaTraining

## What this repo is

A migration of the company's SharePoint OneNote L&D notebook ("KX Training - Delta Platform") into git-friendly markdown. The notebook is an 8-section onboarding course for the Delta Platform (KDB/kdb+ based). Source: SharePoint site `EPAMKXServices`, notebook `Modules.one`.

## Why this exists (4 goals)

1. **Diffable content** — real git diffs instead of an opaque OneNote binary.
2. **AI-assisted review** — Claude/other tools can read and critique the lesson content directly.
3. **MCQ generation** — the lesson markdown is meant to be fed to Claude to generate quiz questions.
4. **Stretch: Playwright video walkthroughs** — automate recorded walkthroughs from the lessons' step-by-step instructions.

## Structure

```
lessons/<NN-section-slug>/
  README.md                 # only when the section is a stub or has a preserved planning outline
  <lesson-id>-<slug>.md      # one file per lesson, e.g. 4.5.5-operating-a-process-cli-optional.md
  images/                    # extracted screenshots/diagrams for that section
```

Section numbering follows the source notebook (01 through 08). Lesson IDs match the source's own numbering, including non-sequential ones like `4.5.5`.

## Conventions used when writing/editing lesson files

- **Reviewer notes**: the source notebook has inline "@person - comment" review threads between the author and reviewers. These are preserved verbatim but moved to a trailing blockquoted section titled `> **Reviewer notes from source notebook (not lesson content):**` at the bottom of the file — never mixed into the teaching content itself. Keep doing this for any lesson not yet migrated or re-migrated.
- **Video placeholders**: the source has several explicit video placeholders (`[Add video]`, `<will add video...>`, a heading noting "this will need to be represented heavily via visuals", etc.) and a few lessons have actual embedded video files. Per instruction, embedded videos were *not* downloaded/transcribed — only flagged inline as a blockquote noting the video's title/topic, tagged as a candidate for the Playwright stretch goal. If asked to resume handling videos, check these flagged spots first.
- **Missing/incomplete source content**: some lessons have blank table rows, placeholder brackets (`[image of...]`), or promised-but-missing worked examples. These are flagged inline as a blockquoted `> **Note:**` rather than invented or silently dropped. Don't fabricate content to fill these gaps.
- **Typos in the source**: a few lessons have a body heading that doesn't match the page/nav title (e.g. says "Module 3" when it's actually Module 4). These are noted with a `> **Note:**` line rather than silently "corrected" — the nav/page title wins as the source of truth.
- **Links**: the OneNote editor renders as a canvas, so most hyperlink hrefs aren't extractable from the page — only links whose destination is also the literal visible text (e.g. a pasted URL) were captured. Everything else is noted as "(link not captured from source — canvas-rendered page, no extractable URL)". Never fabricate or guess a URL to fill these in.
- **Images**: extracted via OneNote's right-click → **Save As** (lossless, full original resolution), not screenshots — screenshots truncate anything wider/taller than the viewport. See memory `onenote-image-extraction` for the full technique if re-running extraction from the live notebook.

## Known environment quirk

Pushing to the GitHub remote (`git remote add` / `git push`) is blocked by this sandbox's permission classifier regardless of in-chat approval. Local commits work fine; pushing needs the user to run it themselves, or add a Bash permission rule. Don't retry it repeatedly — hand the exact commands to the user instead.

## Remote

`https://github.com/GuanyulimFD/delta_platform_training.git` (private)
