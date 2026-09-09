# AI Handoff

Last updated: 2026-09-09, by Claude — second turn, restructuring the template
after `unibo-fc-isi-ds/template-final-report`.

## State

The template compiles in both of its states, with a clean final pdfLaTeX pass:
6 pages of A4 with the guidance on, 2 pages — the bare skeleton — with
`\templateguidanceoff` uncommented. Version 0.2.0.

Nothing has been pushed. `origin` is configured to the DISI GitLab, but the
GitLab project does not exist yet — creating it is Andrea's call, and the first
push is what would create it.

## What the second turn did

Restructured `report.tex` after the newer Distributed Systems template,
`unibo-fc-isi-ds/template-final-report`, taking its *shape* and not its content:
guidance as probing questions rather than prose; a features section asking what
is relevant **and what is not**; an AI-and-tools disclaimer; LaTeX advice moved
to the front; self-evaluation for group work; future works split out.

The new **Relevant agent and MAS features** section is the substantive addition,
and has no counterpart in either source. Its nine features follow the vocabulary
of the course — BDI, computational logic and logic programming, the Linda
coordination primitives, the treatment of truth — as it stands today, so **the
list is provisional** and should be revised as the course settles.

`\guidance` became an environment (`comment` package) so it could hold lists and
floats. Note the trap recorded in `CLAUDE.md`: a heading whose whole body is
guidance has to sit inside the environment, or turning guidance off leaves the
heading behind — which is exactly what happened on the first attempt.

## What the first turn did

Seeded from `pikalab-unibo/report-template` (cloned at
`~/GitHub/pikalab-unibo/report-template`), Andrea's own choice of starting point.

Carried over unchanged: `code-listings.sty`, `prolog-style.sty`, `.gitignore`,
`figures/universe.jpg`, `listings/HelloWorld.java`.

Written new: `report.tex`, `style.sty`, `course.sty`, `references.bib`,
`README.md`, `CLAUDE.md`, this file.

The substantive change is the **section skeleton**. The source template is
shaped as a software-engineering pipeline — requirements, design, deployment,
tests — which fits only one of the three kinds of project the course admits.
The course admits projects concerning theoretical, technological or
methodological aspects, so the skeleton was rebuilt as a common spine with
per-kind guidance, and the software-only sections are marked as such.

## Open — needs Andrea

These were left rather than guessed:

0. **Proportion.** The newer DS template is 590 lines for a full course project;
   this one is about half that for an *optional* project worth 6/30. If it still
   asks more than 6 marks deserve, the sections to thin are *Design* and
   *Validation*.

1. **Whether to create the GitLab project at all**, and whether the
   GitLab-primary/GitHub-mirror arrangement of his other repos applies here. A
   student-facing template may want to be public.
2. ~~**CI.**~~ Settled 2026-09-09: `.gitlab-ci.yml` was deleted. The instance
   does have an online shared runner (`RunnerZero`, id 1, `instance_type`, takes
   untagged jobs), but its *executor* could not be confirmed without an API
   token, and `image:` only works on a Docker/Kubernetes one. The deciding
   argument was not the unknown: this is a template students copy, so a broken
   pipeline would go red in their forks, over a PDF that builds locally in one
   command. If the course later wants a published PDF, that belongs in the
   teacher's copy, not in the students' template.
3. **Language.** Written in British English. If students report in Italian,
   `style.sty` needs `babel` switched.
4. **Course policy the template hints at but does not state**: group size,
   length limit, deadline, delivery channel, and whether the report is delivered
   with the artefacts or separately.
5. **The placeholder assets.** `figures/universe.jpg` and
   `listings/HelloWorld.java` came from the source template; a Prolog or
   AgentSpeak listing would suit this course better than Java.
