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
- `references.bib` is **hand-maintained**. Never wire it to a reference manager,
  and never invent an entry: copy from the course bibliography
  (`ia2627-slides/bib/ia.bib`) and keep the key and the `apice` field.
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
  `references.bib`, `rm -f report.bbl` before rebuilding, or a fixed `.bib` will
  appear still broken.
- **cleveref does not know `lstlisting`.** `\crefname`/`\Crefname` for it are
  declared in `style.sty`; without them every `\cref` to a listing warns.
- The build log has several pdfLaTeX passes. Undefined-reference warnings in the
  early ones are normal — judge the build by the **final** pass.

## Year rollover

Everything course-dependent is in `course.sty`. Rolling the template over to the
next academic year should touch that file and nothing else.
