---
name: aaif-taxonomy-contributions
description: Guides agents through contributing to the AAIF Common Taxonomy and Landscape workstream (aaif/ws-taxonomy-landscape). Use when proposing a definition for an accepted taxonomy term, proposing a new glossary term, adding or fixing an entry on the ecosystem landscape, or helping a contributor pick the right submission path for any of those.
metadata:
  author: Asish Singh
  organization: AAIF
  source: https://github.com/aaif/ws-taxonomy-landscape/blob/main/docs/data-schemas.md
  version: "1.0"
---

# AAIF Taxonomy and Landscape Contributions

Use this skill when helping a contributor propose anything to the AAIF Common Taxonomy and Landscape workstream at `aaif/ws-taxonomy-landscape`. The workstream maintains the shared vocabulary (taxonomy) and ecosystem map (landscape) for all AAIF working groups. Routing a proposal down the wrong path is the most common failure, so start with the routing table.

## Route the contribution first

| The contributor wants to | Correct path |
| --- | --- |
| Supply a definition for a term that is already in `taxonomy/taxonomy-data.js` with the pending placeholder | Open an ISSUE titled `Define: <Term>`, not an ad hoc PR. The repo defers `definition`, `category`, and `broaderTerm` on purpose and its docs ask that proposals for these fields go to an issue or the weekly sync. |
| Propose a brand new glossary term | PR editing `taxonomy/taxonomy-data.js` (for git users), or an issue with the raw details (for everyone else). New entries still leave the deferred fields blank. |
| Add, correct, or update a tool, protocol, or standard on the landscape | PR editing `landscape/landscape.yml`. |
| Question the process, ownership, or placement of something | Issue, or the weekly workstream sync (Mondays, 08:30 PST). |

## Before drafting anything

1. Fetch the current `docs/data-schemas.md` and the header comment of `taxonomy/taxonomy-data.js`. Rules there override this skill if they have changed.
2. Check the term's current entry. Is it accepted with a pending definition, absent entirely, or already defined? That decides the route above.
3. Search open PRs and issues for the same term or tool. In flight proposals exist more often than you expect. If one exists, reference it openly in your proposal and offer reconciliation instead of racing it.
4. Check whether the proposed term duplicates an existing concept. A genuine synonym belongs in the existing term's `aliases` array, but never fold a look alike term into an alias without written sign off from the owning working group's Domain Editor. Deliberately distinct concepts stay separate entries.

## The quality bar for definitions

The bar the workstream has converged on was put memorably by the author of its issue #43, a definition earns its place by naming what would make it false, not what the thing is for. Build each definition around one discriminator a reader can test against a borderline case. Definitions must be vendor neutral, objective, and free of product names or marketing language.

When a term has a contrasting counterpart (Tool and Skill, for example), each term's definition must itself state how it differs from the counterpart, and the pair must be linked through `relatedTerms` or `contrastsWith`. A shared scopeNote that merely records both views writes the confusion down instead of resolving it.

Point `relatedTerms` and `contrastsWith` only at terms already in the taxonomy. By the precedent set in issues #43 and #47, a definition proposal should not smuggle in new terms. If a needed term is missing, say so and propose it separately.

## The Define issue shape

Model definition proposals on the repo's accepted precedent (see issues numbered in the forties for live examples). The shape is

1. One short paragraph noting the term is accepted with a pending definition and that the schema doc asks for an issue rather than a PR, so this is an issue with PR ready text.
2. `## Proposed definition` as a single quoted sentence.
3. `## Why this wording` explaining the discriminator and walking through two or three near misses the definition correctly excludes.
4. `## Proposed scopeNote` capturing boundaries and cross group perspectives.
5. `## Proposed field values` as a code block showing the full entry, with `category`, `broaderTerm`, and any untouched fields explicitly marked unchanged.
6. A disclosure paragraph if the contributor has any stake in how the term lands, plus a note on any overlapping open PR or issue found in step 3 above.

## Schema quick reference

- Terms use sentence case and must be unique across the file.
- Deferred fields on every entry, until the workstream lifts the deferral. `definition` uses exactly the pending placeholder string from the schema doc, `category` is `''`, `broaderTerm` is `null`.
- `workgroups` never contains `Universal`. A term owned by no single group carries `[]`.
- Landscape items require `name`, `homepage_url` (https only), `description` (objective, and the schema doc bans the superlatives "first," "best," "industry-leading," and "revolutionary"), and `project` (one of `graduated`, `incubating`, `member`, `external`). `repo_url` is optional. Live entries also carry fields the schema doc does not list, such as `logo`, so mirror the fields of neighboring entries in `landscape.yml` rather than trusting the doc alone.

## What happens after submission

Merging needs approval from two or three Domain Editors from different working groups, then a workstream Chair merges. Contested or cross cutting proposals go to the Monday sync. If editors deadlock for 14 days, the Chairs arbitrate. Set the contributor's expectations accordingly and suggest the sync when an issue gets no traction.
