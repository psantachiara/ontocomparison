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

The version bar at the top scopes every plane. Excluding states is the analytically useful
operation — drop Insert and p21 and what remains is the public register on its own. The strip
glyph always shows all five cells, greying the excluded ones.

## Relation types

Arcs carry a `rel` tag, assigned at load:

- **influence** — descent. These alone order the vertical axis of the drawings.
- **siting** — a movement's place. Barr writes "CUBISM / 1906-08 Paris" as one block, so the
  city is an attribute at the same height, not a successor.
- **membership** — a movement's personnel.

Drawings distinguish the three; **the metrics do not** — PageRank, density and consensus count
all arcs together. That is why Paris ranks first on the jacket, and it is a coding choice worth
arguing about in the paper rather than a property of Barr's chart.

## The year axis

Vertical position **is** the date, on the same linear scale Barr ruled on both margins of his
sheets. Equal vertical gaps are equal spans of time. Horizontal position carries no meaning —
it is barycentre ordering, arranged to minimise crossings.

Nothing is banded and nothing is nudged downward to tidy the drawing, so **an arc that runs
backwards in time is drawn in red and counted in the graph header**. A violation is a
contradiction in the coding, almost always a mis-dated concept, and is meant to be fixed in the
data rather than hidden by the layout. Building this axis caught eight bad dates in the shipped
reconstruction on its first run.

Names in faint italic are not positioned by date. Cities and personnel carry no date in the
chart's logic, so they sit at the median date of whatever they are attached to.

## Facsimiles

Create an `img/` folder beside `index.html` containing `p15.jpg`, `insert.jpg`, `p19.jpg`,
`p21.jpg` and `cover.jpg`. Each States card loads its own image automatically and falls back to
an instruction placeholder when the file is absent; clicking opens the full-size image.
File names follow the version `id`, so a renamed or added state needs a matching file. A
`facsimile` path set explicitly in the dataset overrides the convention.

The MoMA Archives sheets (AHB VI.A.38) carry a study-use restriction — check your rights before
publishing a page that serves them.

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

Facsimile images are **not** included in this folder. See *Facsimiles* above.
