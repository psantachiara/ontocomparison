# Five States of a Chart

An interactive five-plane comparison instrument for Alfred H. Barr, Jr.'s successive chart drafts
for *Cubism and Abstract Art* (MoMA, 1936): **p15, Insert, p19, p21, Cover**.

## Deploying to GitHub Pages

The instrument is one self-contained file. Push this folder to a repository and enable Pages:

```
Settings → Pages → Source: Deploy from a branch → main / (root)
```

`index.html` has no build step and no dependencies beyond two Google Fonts loaded at runtime.
Everything else — layout, PageRank, Jaccard, consensus thresholding, community detection,
edit-grammar coding — is computed in the browser from a single dataset object.

## The five planes

| | Plane | What it compares |
|---|---|---|
| I | Terminological | Surface labels, variants, relabelling and typographic restyling |
| II | Conceptual | Extension and composition; Jaccard; core and hapax sets |
| III | Structural | Layered DAGs, degree, density, PageRank divergence, clusters |
| IV | Genetic | Similarity against draft order, consensus thresholds, edit grammar |
| V | Pragmatic | Support, audience, permanence, constraint, rhetorical function |

Planes IV and V are proposed additions to the existing terminological/conceptual/structural
framework, and they carry the argument: the series is not one line of refinement, and the
published state's shape has a material cause.

## Replacing the dataset

`barr-dataset.json` is the shipped reconstruction. Edit it against your own coding and load it
back through **Method & provenance → Load dataset**; every plane recomputes. Five keys:

- `concepts` — `id: {l: label, t: movement|source|person|place, y: year}`
- `versions` — per state: `nodes`, `edges`, `labels` (surface variants), `pragmatic`, `facsimile`
- `members` — movement → persons, expanded into arcs at load
- `skeleton` — influence relations shared across the developed charts
- `sited` — concept → places, expanded into arcs at load

Storing membership and siting once means a personnel correction is a one-line edit rather than
forty. Set `explicitOnly: true` on a state to suppress skeleton/member/siting expansion.

An integrity check runs on load and reports any back-edges removed. Zero is the number you want;
anything else means the coding asserts that A precedes B and B precedes A.

## Provenance

**The shipped dataset is a reconstruction, not the authoritative coding.** Node and arc sets were
rebuilt from the chart facsimiles and from the tables printed in Leazer, "The Development and
Comparison of Small-Scale Classifications for Knowledge Organization," NASKO, 20 June 2025.
Where the two disagree, the figure is shown in red beside the published value. Arc-level fidelity
is lowest for p15 and p21, the annotated sheets.

Facsimiles are **not** included: the MoMA Archives sheets (AHB VI.A.38) carry a study-use
restriction. Each state has an empty `facsimile` field — point it at a local file if your rights
permit, and the card will render it.
