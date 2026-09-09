# Notes for Claude

Conventions and traps for this repository. Reasoning that a *reader* needs is in
`README.md`; this file is what an agent needs before editing.

## What this is

A student-facing LaTeX **template**, not a document. Two consequences:

- Keep the surface small. Every package added here is a package a student may
  have to debug on whatever TeX installation they happen to use.
- Prose in the template is *instruction to the student*, and belongs in a
  `\guidance{…}` box so `\templateguidanceoff` can remove it. Do not write
  instructions as ordinary body text.

## House rules that apply here

- `.tex` and `.sty` take **very short comments** — a line or two per block,
  saying what the block is and how it is called. Reasoning goes to `README.md`,
  traps here, state to `.ai/HANDOFF.md`.
- Keep the `%%%% … by Andrea Omicini <mailto:…>` header on every `.tex`/`.sty`.
- `references.bib` is **hand-maintained**. Never wire it to a reference manager,
  and never invent an entry: copy from the course bibliography
  (`ia2627-slides/bib/ia.bib`) and keep the key and the `apice` field.
- Markdown must pass markdownlint cleanly before the work is called done.

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
