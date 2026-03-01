# Clean Resubmit Plan from Closed PRs (#20/#21/#22)

## Context
Feedback from maintainer indicates 3 PRs were closed mainly due to extra/generated artifacts mixed with useful edits.

- Closed: `#20` (review dossiers only), `#21` (ToC/table syntax), `#22` (end markers + lint script)
- Merged separately: `#23..#27`

## Goal
Extract only valuable syntax corrections from closed PRs and resubmit as minimal, noise-free patches:

- only `FPF-Spec.md` in fix PRs,
- no `review/*` dossier files,
- no `scripts/*` lint files.

## Useful fixes still visible on current upstream main

### 1) Markdown row not closed (parser risk)
- Evidence: `FPF-Spec.md:61` (`A.6.C` row has no trailing `|`).
- Proposed fix: close the row with final `|`.

### 2) Table cell split by unescaped pipe in E.16 row
- Evidence: `FPF-Spec.md:229` has `..., UTS | *Queries:* ...` inside row content.
- Proposed fix: replace inner `|` with punctuation (e.g., `UTS.`) so the row keeps column shape.

### 3) Unescaped literal pipes in row content
- Evidence:
  - `FPF-Spec.md:94-99` (`pass|degrade|abstain` in ToC table cells),
  - `FPF-Spec.md:279` (`{pass|degrade|abstain}` in ToC row).
- Proposed fix: escape literal pipes in table-cell text (`\|`) only where they break table parsing.

### 4) Section end marker mismatch C.25
- Evidence:
  - `FPF-Spec.md:32104` section is `C.25`,
  - `FPF-Spec.md:32109` closes as `### C.23:End`.
- Proposed fix: `C.23:End -> C.25:End`.

### 5) Section end marker mismatch E.13
- Evidence:
  - `FPF-Spec.md:35241` starts `## E.14`,
  - `FPF-Spec.md:35239` closes previous as `### E.10:End` (should close E.13).
- Proposed fix: `E.10:End -> E.13:End`.

## What to avoid in resubmission
- No bundled analysis/roadmap markdown in the same PR.
- No helper scripts in same PR (`scripts/lint_section_end_markers.sh` was a rejection trigger).
- No broad "global escape everywhere" edits; keep delta strictly to proven parser-break lines.

## Suggested PR split
1. `fix: minimal table-parser repairs in FPF-Spec`
   - includes items 1,2,3 above.
2. `fix: section end marker consistency in FPF-Spec`
   - includes items 4,5 only.

This split keeps review scope narrow and aligns with maintainer preference for small, clean diffs.
