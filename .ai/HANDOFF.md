# AI Handoff

Last updated: 2026-09-09, by Claude — the turn that created this repository.

## State

The template compiles: `latexmk -pdf report.tex` produces a 4-page A4
`report.pdf`, and the final pdfLaTeX pass is free of warnings and errors, with
every cross-reference resolved.

Nothing has been pushed. `origin` is configured to the DISI GitLab, but the
GitLab project does not exist yet — creating it is Andrea's call, and the first
push is what would create it.

## What this turn did

Seeded from `pikalab-unibo/report-template` (cloned at
`~/GitHub/pikalab-unibo/report-template`), Andrea's own choice of starting point.

Carried over unchanged: `code-listings.sty`, `prolog-style.sty`, `.gitignore`,
`figures/universe.jpg`, `listings/HelloWorld.java`.

Written new: `report.tex`, `style.sty`, `course.sty`, `references.bib`,
`README.md`, `CLAUDE.md`, this file.

The substantive change is the **section skeleton**. The source template is
shaped as a software-engineering pipeline — requirements, design, deployment,
tests — which fits only one of the three kinds of project the course admits.
The A0 deck says a project "may concern theoretical / technological /
methodological aspects", so the skeleton was rebuilt as a common spine with
per-kind guidance, and the software-only sections are marked as such.

## Open — needs Andrea

These were left rather than guessed:

1. **Whether to create the GitLab project at all**, and whether the
   GitLab-primary/GitHub-mirror arrangement of his other repos applies here. A
   student-facing template may want to be public, unlike `ia2627-slides`.
2. **CI.** `.gitlab-ci.yml` is written but *unverified*: whether DISI GitLab
   offers runners to this namespace is unknown, and an always-red pipeline in a
   template students copy is worse than no pipeline. Delete it or verify it.
3. **Language.** Written in British English, following the decks. If students
   report in Italian, `style.sty` needs `babel` switched.
4. **Course policy the template hints at but does not state**: group size,
   length limit, deadline, delivery channel, and whether the report is delivered
   with the artefacts or separately.
5. **The placeholder assets.** `figures/universe.jpg` and
   `listings/HelloWorld.java` came from the source template; a Prolog or
   AgentSpeak listing would suit this course better than Java.
6. **A latent bug in `ia2627-slides/bib/ia.bib`**: entry `rao-agentspeak96` has
   `month = {{22--25~} # jan}`, whose doubled braces make the `#` literal. It is
   corrected in this repo's copy but not at the source, where it will break any
   build that formats that entry's month.
