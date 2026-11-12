# deltaTraining

## What this repo is

A migration of the company's SharePoint OneNote L&D notebook ("KX Training - Delta Platform") into git-friendly markdown. The notebook is an 8-section onboarding course for the Delta Platform (KDB/kdb+ based). Source: SharePoint site `EPAMKXServices`, notebook `Modules.one`.

**Section 1 is the exception**: the source notebook's Section 1 was an empty stub (title + date only). It was authored fresh, collaboratively with the user, rather than migrated — see "Section 1 is different" below before touching it.

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

## Section 1 is different

Unlike Sections 2–8, Section 1 ("Introduction to Delta Platform") has no OneNote source — it was written from scratch in collaboration with the user, grounded in (a) the content of Sections 2–8 themselves and (b) the official docs at https://code.kx.com/platform/latest/. None of the Sections 2–8 conventions above apply to it:

- No "Reviewer notes" blockquotes (no source reviewer comments exist).
- No "Note:" fidelity flags for typos/gaps (nothing to be faithful to — if something reads wrong, just fix it).
- Its one diagram (`1.2-...images/1.2-delta-platform-architecture.svg`) was hand-authored as SVG, not extracted. Audience for the whole section: new joiners roughly 1–2 months into kdb+/q training up to ~1.5 years' experience, who likely haven't seen a hand-rolled production kdb+ system before — so the "how is this different from native kdb+" framing in 1.1 briefly sketches what a from-scratch setup looks like rather than assuming the reader has already seen one.
- When adding new content to Section 1 or touching the diagram, preview SVGs before finalizing by serving the scratchpad dir with `python3 -m http.server` and opening a tiny wrapper HTML (`<img src="...svg">`) in a Claude-in-Chrome tab — the extension can't screenshot a raw `file://` or bare `image/svg+xml` response directly.

## Known environment quirk

Pushing to the GitHub remote (`git remote add` / `git push`) is blocked by this sandbox's permission classifier regardless of in-chat approval. Local commits work fine; pushing needs the user to run it themselves, or add a Bash permission rule. Don't retry it repeatedly — hand the exact commands to the user instead.

## Remote

`https://github.com/GuanyulimFD/delta_platform_training.git` (private)
