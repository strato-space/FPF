# Sequential PR Apply (No Conflicts) — 2026-03-01

## Goal
Make the `#20..#27` fix stack apply cleanly in strict sequence for a non-git-specialist workflow.

## Final apply order
1. `docs/deep-review-2026-03-01` (`d66bbcf`)
2. `fix/13-toc-table-schema` (`fbf0349`)
3. `fix/14-section-end-markers` (`6bc1e03`)
4. `fix/15-duplicate-subsection-ids` (`777cef0`)
5. `fix/16-id-style-drift` (`f27ded5`)
6. `fix/17-status-enum-drift` (`6fb1a61`)
7. `fix/18-part-f-table-integrity` (`748fbf3`)
8. `fix/19-editorial-drift` (`13abb61`)

## What was repacked to remove conflicts
- `fix/13-toc-table-schema` was repacked to include nearby `E.15` status normalization (overlap hot-spot with `fix/17`).
- `fix/17-status-enum-drift` now contains only non-overlapping status fixes.
- `fix/18-part-f-table-integrity` now contains only unique malformed-row repairs (`A6`/`A11` table rows) and no duplicate tri-state escaping edits.

## Verified result
- Sequential `cherry-pick` of all 8 branches on fresh `origin/main` completed with no conflicts.
- Integrated branch pushed to fork:
  - `integration/all-prs-20-27-20260301` at `6a23674`.
- Conflict marker check:
  - `rg '^(<<<<<<<|=======|>>>>>>>)' FPF-Spec.md` -> no matches.

## Non-specialist apply commands
```bash
git fetch origin --prune
git checkout -B integration/all-prs-20-27-20260301 origin/main
git cherry-pick \
  origin/docs/deep-review-2026-03-01 \
  origin/fix/13-toc-table-schema \
  origin/fix/14-section-end-markers \
  origin/fix/15-duplicate-subsection-ids \
  origin/fix/16-id-style-drift \
  origin/fix/17-status-enum-drift \
  origin/fix/18-part-f-table-integrity \
  origin/fix/19-editorial-drift
```

## Text body hygiene check
- Checked created `issues/PRs` in `ailev/FPF` (`#11..#27`) for literal `\\n` sequences in bodies.
- Result: no literal `\\n` artifacts found.
