# Project report template — Intelligent Agents 2026/2027

The LaTeX template for the report on the **optional project** of the course of
Intelligent Agents, Academic Year 2026/2027 — Andrea Omicini and Giovanni
Ciatto, DISI, Alma Mater Studiorum – Università di Bologna.

The project is optional and worth up to 6/30. It must cover, or follow from, a
specific topic of the course, and it must be agreed with the teachers
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

The result is `report.pdf`. The template needs pdfLaTeX and BibTeX and nothing
else — no shell-escape, no external tool, nothing to install beside the sources.

It does need a **full TeX Live**. Beyond the usual LaTeX packages it loads
[`acro`](https://ctan.org/pkg/acro),
[`cleveref`](https://ctan.org/pkg/cleveref) and
[`comment`](https://ctan.org/pkg/comment), which TeX Live keeps in
`collection-latexextra`, and of the four installation schemes only the full one
brings that collection in — not basic, not small, not medium. So: MacTeX, or
TeX Live installed with the full scheme, or `texlive-full` on Debian and Ubuntu.
On a smaller installation, `tlmgr install acro cleveref comment` is enough to
make up the difference.

On GitLab, `.gitlab-ci.yml` runs that same command on every push and leaves
`report.pdf` as a downloadable artifact — so a report that compiles for you
compiles on a clean machine too. Artifacts are dropped after four weeks, which
costs nothing: the PDF is a few seconds of `latexmk` away. The pipeline needs
nothing from you, and if you would rather not have it, delete the file.

## Layout

| path | what it holds |
| --- | --- |
| `report.tex` | the report: the sections you fill in |
| `sty/` | the style files |
| `bib/references.bib` | the bibliography |
| `img/` | figures |
| `lst/` | source code to be included in the report |

Put your own figures in `img/` and your own code in `lst/`. Only
`report.tex` sits at the top level; if you split the report into several files,
keep them there beside it.

`report.tex` points LaTeX at `sty/` in its second line, which is what lets
`\usepackage{style}` find `sty/style.sty`. If you add a style file of your own,
put it in `sty/` and load it the same way, by its plain name and without a
`\ProvidesPackage` line.

## The three kinds of project

A project may have a mostly **theoretical**, **technological** or
**methodological** focus. The sections are a common spine, and each says what it
expects from each kind.

Since a project is assessed on **technical** skill, the technology is prominent
whatever the focus, and every kind builds something: a theoretical project
argues a model and builds a proof of concept, a technological one builds an
intelligent system as a multi-agent system, a methodological one prescribes a
method and builds a case study.

One section deserves attention whatever the kind. **Relevant agent and MAS
features** asks you to argue which agent-oriented features bear on your project
*and which do not*: intelligence, autonomy and agency; the symbolic, the
subsymbolic and the non-symbolic; goal-directedness and mental states;
reactivity and situatedness; sociality, interaction and coordination; reasoning
and inference; knowledge and truth; learning and adaptation; openness and
heterogeneity; and tools. The list is open — add whatever else your project
explores. The exclusions matter as much as the inclusions — a feature dismissed
with a reason shows the design was thought about — and whatever you claim there
is what the rest of the report has to deliver.

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

Cite with `\cite`, giving the key of an entry in `bib/references.bib`. One entry
is there as an example — the book of the course — and it can go once you have
your own.

The style is `apalike`, so a citation prints author and year rather than a
number: `[Mascardi and Omicini, 2026]`. Do not load `natbib` on top of it —
`sty/style.sty` says why, in the comment where it used to be loaded.

Ready-made BibTeX entries for most computer science papers can be copied from
[DBLP](https://dblp.org/); entries for the papers of the course are on
[APICe](https://apice.unibo.it/). Cite the works you actually used, and cite
them from the point in the text where they are used.

## Credits

Derived from the final report templates of the Distributed Systems and Intelligent
System Engineering courses,
[`pikalab-unibo/report-template`](https://github.com/pikalab-unibo/report-template)
and
[`unibo-fc-isi-ds/template-final-report`](https://github.com/unibo-fc-isi-ds/template-final-report).
