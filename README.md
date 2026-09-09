# Project report template — Intelligent Agents 2026/2027

The LaTeX template for the **optional project report** of the course of
Intelligent Agents, Academic Year 2026/2027 — Andrea Omicini, DISI, Alma Mater
Studiorum – Università di Bologna, Cesena campus.

The project is optional, worth up to 6/30, and assesses the *practical*
knowledge of the student. It must cover, or follow from, a specific topic of the
course, and must be negotiated with the teacher beforehand. See the
[Projects page on APICe](https://apice.unibo.it/xwiki/bin/view/Course/Iag2627/Projects).

## Building

```bash
latexmk -pdf report.tex     # or: pdflatex report && bibtex report && pdflatex report && pdflatex report
```

The template compiles with pdfLaTeX and BibTeX only — no shell-escape, no
external tooling, and no dependency on anything installed outside the repo —
so it builds unchanged on any standard TeX installation. Output is
`report.pdf`, which is git-ignored.

## Layout

| file | what it holds |
| --- | --- |
| `report.tex` | the report itself: the section skeleton students fill in |
| `course.sty` | every course-dependent string — the only file to touch on year rollover |
| `style.sty` | packages, the `\emailaddr` and `\guidance` macros |
| `code-listings.sty` | `listings` setup and the `\javaimport` / `\prologimport` / … macros |
| `prolog-style.sty` | Prolog syntax highlighting |
| `references.bib` | the bibliography |
| `figures/`, `listings/` | placeholder assets for the worked examples |

## The three kinds of project

The course admits **theoretical**, **technological** and **methodological**
projects, and they do not fill a report in the same way. The section skeleton is
therefore a common spine — goal, background, contribution, validation,
conclusions — rather than the software-engineering pipeline of the template this
one derives from. Each section carries a `\guidance` box saying what it expects
from each of the three kinds, and *Design*, *Implementation* and *Deployment and
usage* are marked as belonging to technological projects only.

Sections that do not apply should be **dropped, not left empty**.

## The guidance boxes

Every instruction in the template is wrapped in `\guidance{…}`, typeset small and
italic. Once the report is written, one line in the preamble removes them all:

```latex
\templateguidanceoff
```

This keeps a single source: there is no separate "instructions" and "clean"
variant of the template to drift apart.

## The bibliography

`references.bib` holds two entries, copied from the course bibliography as
worked examples of the house format: hand-maintained, stable citation keys, and
an `apice` field cross-referencing the entry into APICe. Replace them.

Two traps live here, both of which cost a build during setup:

- **No header comment.** BibTeX scans for `@` to find the next entry, and the
  `@` in a `mailto:` address inside a leading `%%%%` comment block is read as the
  start of an entry. This is why the course `.bib` files carry no header, and
  neither does this one.
- **Concatenation braces.** `month = {22--25~} # jan` concatenates a string with
  the `jan` macro. Writing `month = {{22--25~} # jan}` instead makes the `#`
  *literal text*, which reaches LaTeX raw and aborts the build with
  `You can't use macro parameter character #`. The entry copied from `ia.bib`
  carried the doubled braces and was corrected here.

## Provenance

Derived from [`pikalab-unibo/report-template`](https://github.com/pikalab-unibo/report-template),
the final-report template of the Distributed Systems courses. Kept from it: the
`listings` configuration and import macros, the Prolog style, the `.gitignore`,
the stylistic notes, and the version macros. Rewritten: the section skeleton,
the course identity, the style layer, and the bibliography.
