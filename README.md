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
projects, and they do not fill a report in the same way. The skeleton is
therefore a common spine, with per-kind notes in every section, and
*Design*, *Implementation* and *Deployment and usage* marked as belonging to
technological projects only.

Sections that do not apply should be **dropped, not left empty**.

The spine is: Concept -> Background -> Relevant agent and MAS features ->
Contribution -> Validation -> Deployment and usage -> Self-evaluation ->
Conclusions -> Future works, preceded by a Disclaimer and, while drafting, by
two removable sections of instructions.

### Relevant agent and MAS features

The one section with no counterpart in the templates this derives from, and the
reason for the rewrite. It asks the student to argue which agent-oriented
features bear on the project **and which do not** — autonomy and agency,
goal-directedness and mental state, reactivity and situatedness, sociality and
coordination, reasoning and inference, knowledge and truth, learning and
adaptation, openness and heterogeneity, organisation and norms.

The exclusions carry as much weight as the inclusions: a feature dismissed with
a reason shows the design was thought about, and what is claimed here is what
*Contribution* then has to deliver. The list follows the vocabulary of the
course itself, so it should be revised as the course's own material settles.

## The guidance boxes

Every instruction to the student sits in a `guidance` environment, typeset small
and italic:

```latex
\begin{guidance}
  ... instructions, lists and examples ...
\end{guidance}
```

It is an environment rather than a macro so that it can hold lists, figures and
listings. Uncommenting one line in the preamble removes every one of them:

```latex
\templateguidanceoff
```

This keeps a single source: there is no separate "instructions" and "clean"
variant of the template to drift apart. With the guidance on the document is
6 pages; with it off, 2 — the bare skeleton plus the disclaimer.

Two consequences worth knowing:

- A heading whose whole body is guidance must sit **inside** the environment,
  or turning guidance off leaves an empty heading behind. This is why
  *How to use this template* and *Quick LaTeX suggestions* have their
  `\section*` inside the block, while *Disclaimer* — which has real content —
  does not.
- The environment comes from the `comment` package, which round-trips the block
  through a `comment.cut` scratch file. It is git-ignored already.

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

Derived from two Distributed Systems report templates.

From [`pikalab-unibo/report-template`](https://github.com/pikalab-unibo/report-template),
the original starting point: the `listings` configuration and import macros, the
Prolog style, the `.gitignore`, and the version macros.

From [`unibo-fc-isi-ds/template-final-report`](https://github.com/unibo-fc-isi-ds/template-final-report),
the newer one, the *shape* rather than the content: guidance written as probing
questions instead of prose, a features section that asks what is relevant and
what is not, an AI-and-tools disclaimer, LaTeX advice moved to the front where
it is read before it is needed, self-evaluation for group work, and future works
as a section of its own.

Neither is followed on structure. Both are built around a single software
pipeline — requirements, design, deployment, tests — which fits only the
technological third of what this course admits.
