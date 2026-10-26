# Resources (source material inbox)

Drop raw course material here before asking Claude to draft notes from it — slides, homework PDFs, problem sets exported from Canvas (Tec) or Moodle (Essex), your own scanned/typed lecture notes, etc.

**Convention:** save material under `<domain>/<course>/`, matching where that course's notes live in the vault, e.g. `Resources/07 Finance & Markets/Financial Derivatives/`. A domain that currently holds only one course (`03 Stochastic Processes`, `05 Dynamic Programming & Reinforcement Learning`) skips the course subfolder and takes files directly at the domain root.

If your source material already comes chunked by chapter/topic (most Essex modules do), keep that structure — `<course>/Chapter N - Topic/Lecture Material/`, `.../Exercises & Solutions/`, `.../Past Papers/`, etc. — rather than flattening it. It mirrors how you'll want to work through a course batch-by-batch anyway. For a one-off file with no natural chapter home, the flat fallback still works: `<Course> - <what it is> - <YYYY-MM>.<ext>`.

This folder is git-ignored-friendly for large binaries if you'd rather not version them — see the strategy note for the recommended `.gitignore` tweak. Nothing in here needs to be perfectly organized before you start; even a partial drop lets Claude ground the notes it touches instead of guessing.

**Last reorganized:** 2026-09-17 — a bulk drop of course material had landed entirely under `01 Mathematical Foundations` (named by Tec/Essex course code, e.g. `MA2008B`, `MA319_StochasticProc`) regardless of actual domain. It was re-sorted into the correct domain folders and renamed to match each course's note folder name. See the strategy note §8 for the full mapping.
