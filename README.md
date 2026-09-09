# Project report template — Intelligent Agents 2026/2027

The LaTeX template for the report on the **optional project** of the course of
Intelligent Agents, Academic Year 2026/2027 — Andrea Omicini, DISI, Alma Mater
Studiorum – Università di Bologna.

The project is optional and worth up to 6/30. It must cover, or follow from, a
specific topic of the course, and it must be agreed with the teacher
beforehand. See the
[Projects page on APICe](https://apice.unibo.it/xwiki/bin/view/Course/Iag2627/Projects).

## Getting started

1. Get a copy of this repository, and work in it.
2. Put your title and the names and addresses of the authors at the top of
   `report.tex`.
3. Write the report, following the instructions in the template.
4. When you are done, uncomment `\templateguidanceoff` in the preamble: all the
   instructions disappear, and what is left is your report. Read it once in that
   state before handing it in.

## Building

```bash
latexmk -pdf report.tex
```

Or, by hand:

```bash
pdflatex report && bibtex report && pdflatex report && pdflatex report
```

The template needs pdfLaTeX and BibTeX and nothing else — no shell-escape, no
external tool, and nothing installed outside the repository — so it builds on
any standard TeX installation. The result is `report.pdf`.

On GitLab, `.gitlab-ci.yml` runs that same command on every push and keeps
`report.pdf` as a downloadable artifact for four weeks — so a report that
compiles for you compiles on a clean machine too. It needs nothing from you,
and if you would rather not have it, delete the file.

## Layout

| path | what it holds |
| --- | --- |
| `report.tex` | the report: the sections you fill in |
| `sty/` | the style files |
| `bib/references.bib` | the bibliography |
| `img/` | figures |
| `listings/` | source code to be included in the report |

Put your own figures in `img/` and your own code in `listings/`. Only
`report.tex` sits at the top level; if you split the report into several files,
keep them there beside it.

`report.tex` points LaTeX at `sty/` in its second line, which is what lets
`\usepackage{style}` find `sty/style.sty`. If you add a style file of your own,
put it in `sty/` and load it the same way, by its plain name and without a
`\ProvidesPackage` line.

## The three kinds of project

A project may be **theoretical**, **technological** or **methodological**, and
the three do not fill a report in the same way. The sections are a common
spine, and each says what it expects from each kind.

*Design*, *Implementation* and *Deployment and usage* concern technological
projects. If yours is not one, **delete them** — a section that does not apply
should be removed, not left empty.

One section deserves attention whatever the kind. **Relevant agent and MAS
features** asks you to argue which agent-oriented features bear on your project
*and which do not*: autonomy and agency, goal-directedness and mental state,
reactivity and situatedness, sociality and coordination, reasoning and
inference, knowledge and truth, learning and adaptation, openness and
heterogeneity, organisation and norms. The exclusions matter as much as the
inclusions — a feature dismissed with a reason shows the design was thought
about — and whatever you claim there is what the rest of the report has to
deliver.

## The instructions in the template

Every instruction sits in a `guidance` block, typeset small and italic:

```latex
\begin{guidance}
  ... instructions ...
\end{guidance}
```

One line in the preamble removes all of them at once:

```latex
\templateguidanceoff
```

Leave them on while you write; turn them off for the version you hand in. Do
not delete them by hand — that way you can turn them back on if you need to
check what a section was asking for.

## Names and acronyms

`sty/names.sty` declares the acronyms and the names of the course, so that each
is written the same way everywhere. Anything with a long form is an
[`acro`](https://ctan.org/pkg/acro) acronym, used through acro's own commands:

```latex
\ac{mas}    % multi-agent system (MAS) the first time, MAS from then on
\acs{mas}   % MAS          \acl{mas}  % multi-agent system
\acf{mas}   % the full form, wherever the first use fell
\acs*{mas}  % the short form in a heading, without spending the first use
```

Anything with no long form is pure typography and is a plain macro in the same
file — `\jason`, `\tuprolog`, `\respect`, `\apice`. Declare what your report
needs there, delete what it does not use, and take anything else you need from
the `sty/names.sty` of the course slides.

## The bibliography

Cite with `\cite`, giving the key of an entry in `bib/references.bib`. Two
entries are there as examples; replace them with your own.

Ready-made BibTeX entries for most computer science papers can be copied from
[DBLP](https://dblp.org/). Cite the works you actually used, and cite them from
the point in the text where they are used.

## Credits

Derived from the final report templates of the Distributed Systems courses,
[`pikalab-unibo/report-template`](https://github.com/pikalab-unibo/report-template)
and
[`unibo-fc-isi-ds/template-final-report`](https://github.com/unibo-fc-isi-ds/template-final-report).
