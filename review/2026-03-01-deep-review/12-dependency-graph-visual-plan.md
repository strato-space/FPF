# Dependency Graph Visual Plan (Deep Dive)

## Artifact
- HTML visual explainer: `review/2026-03-01-deep-review/artifacts/fpf-dependency-deep-dive-2026-03-01.html`
- Raw graph extraction: `review/2026-03-01-deep-review/artifacts/fpf_dep_analysis.json`
- Visual payload used for rendering: `review/2026-03-01-deep-review/artifacts/fpf_visual_payload.json`

## Snapshot
- Branch: `integration/all-prs-20-27-20260301`
- Source file: `FPF-Spec.md`
- Canonical section nodes (`## <ID>`): `170`
- Resolved dependency edges: `518`
- Unresolved referenced IDs (not canonical section nodes): `63`
- Largest SCC sizes: `17`, `13`, `2`

## Key graph signals
- Inbound hubs: `B.3`, `E.10`, `F.1`, `G.5`, `A.15`, `F.9`.
- Outbound hubs: `E.16`, `G.8`, `A.6`, `F.17`, `G.1`, `G.0`.
- Strongest cross-part pressures:
  - `C -> G` (`28`)
  - `B -> A` (`27`)
  - `G -> C` (`22`)
  - `A -> E` (`21`)
  - `G -> E` (`19`)

## Top unresolved IDs by pressure
- `E.10.D1` (`17` refs)
- `A.2.1` (`12` refs)
- `A.1.1` (`11` refs)
- `B.1.4` (`8` refs)
- `A.15.1` (`7` refs)

## Execution phases in visual plan
1. Graph integrity baseline (linters and section/anchor checks).
2. Canonical ID governance (grammar + alias registry + status enum checks).
3. Missing node strategy (stub canonical sections vs explicit roadmap classification).
4. Core cycle reduction (SCC refactor boundaries).
5. Continuous dependency observability (release-by-release drift snapshots).

## Notes
- Visual artifact includes:
  - Cross-part dependency diagram.
  - Core hub topology diagram.
  - Unresolved reference pressure table with line evidence.
  - SCC/cycle table.
  - Detailed phased execution plan with dependency flow.
