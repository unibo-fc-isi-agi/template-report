# Notes for Claude

Conventions and traps for this repository. Reasoning that a *reader* needs is in
`README.md`; this file is what an agent needs before editing.

## What this is

A student-facing LaTeX **template**, not a document. Two consequences:

- Keep the surface small. Every package added here is a package a student may
  have to debug on whatever TeX installation they happen to use.
- Prose in the template is *instruction to the student*, and belongs in a
  `guidance` environment so `\templateguidanceoff` can remove it. Do not write
  instructions as ordinary body text.
- Prefer **probing questions** to descriptive prose. "What is the environment,
  and how does the agent perceive it?" is usable; "this section describes the
  environment" is not.

## House rules that apply here

- `.tex` and `.sty` take **very short comments** — a line or two per block,
  saying what the block is and how it is called. Reasoning goes to `README.md`,
  traps here, state to `.ai/HANDOFF.md`.
- Keep the `%%%% … by Andrea Omicini <mailto:…>` header on every `.tex`/`.sty`.
- `bib/references.bib` is **hand-maintained**. Never wire it to a reference manager,
  and never invent an entry — transcribe it from the source, keeping a stable
  citation key and the `apice` cross-reference field.
- Markdown must pass markdownlint cleanly before the work is called done.

## The guidance environment

- It is an environment, not a macro, so it can carry lists, figures and
  listings. It comes from the `comment` package via `\specialcomment`.
- **A heading whose entire body is guidance must go inside the environment.**
  Otherwise `\templateguidanceoff` leaves an empty heading behind. Check both
  states after touching the front matter: build once as-is, once with
  `\templateguidanceoff` uncommented, and read the second one.
- The package round-trips each block through `comment.cut`. Harmless, ignored.

## Traps

- **No header comment in `.bib`.** BibTeX scans for `@`; the one in a `mailto:`
  inside a leading comment block is parsed as an entry and breaks the run.
- **`#` in `.bib` is concatenation, and braces change that.**
  `month = {22--25~} # jan` is correct; `month = {{22--25~} # jan}` makes the `#`
  literal, and LaTeX aborts on the resulting `.bbl`.
- **`latexmk -C` does not always clear a stale `.bbl`.** After editing
  `bib/references.bib`, `rm -f report.bbl` before rebuilding, or a fixed `.bib` will
  appear still broken.
- **cleveref does not know `lstlisting`.** `\crefname`/`\Crefname` for it are
  declared in `sty/style.sty`; without them every `\cref` to a listing warns.
- The build log has several pdfLaTeX passes. Undefined-reference warnings in the
  early ones are normal — judge the build by the **final** pass.

## Layout

Sources go in directories by kind — `sty/`, `bib/`, `img/`, `listings/` — with
only `report.tex` at the root.

- `report.tex` sets `\input@path` to `{sty/}` so `\usepackage{style}` resolves,
  and so the style files can load each other by plain name. Do not replace this
  with a `latexmkrc` or `TEXINPUTS`: the template must build when typeset
  directly, not only under latexmk.
- **The style files must not declare `\ProvidesPackage`.** With `\input@path`
  in play LaTeX requests them as `sty/style`, `sty/course`, …, so a
  `\ProvidesPackage{style}` mismatches the request and warns on every build.
- Figures are found through `\graphicspath{{img/}}`, set in `sty/style.sty`.
- The bibliography is referenced as `\bibliography{bib/references}`.

## Year rollover

Everything course-dependent is in `sty/course.sty`. Rolling the template over to the
next academic year should touch that file and nothing else.
