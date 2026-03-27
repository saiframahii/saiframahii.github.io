# CLAUDE.md — Occupant-Centric Control Ontology (OCCO)

## Project Identity

**Ontology:** Occupant-Centric Control Ontology (OCCO)
**Namespace:** `https://w3id.org/occo#`
**Persistent URI:** `https://w3id.org/occo`
**Context:** PhD research — Birmingham City University
**Paper:** EC3 2026 conference submission
**Active version:** v0.0.2-dev (348 triples)

---

## Repository Layout

```
saiframahii.github.io/
├── src/              ← LOCAL ONLY — gitignored. OneDrive is the canonical source.
│   ├── v0.0.1/       ← FROZEN — paper submission version, never modify
│   └── v0.0.2/       ← active development; edit TTL here
│       └── evaluation/
│           ├── oops/    ← OOPS! evaluation files
│           └── foops/   ← FOOPS! stub (fill after w3id.org is live)
└── occo/             ← TRACKED — published output served by GitHub Pages
    ├── occo.ttl / occo.rdf
    ├── releases/0.0.1/ and 0.0.2/
    └── evaluation/
        ├── oops/        ← live OOPS report + raw XML
        ├── foops/       ← populate after FOOPS is run
        └── sparql/      ← populate after SPARQL CQs are documented
```

`src/` exists locally as a working copy but is gitignored — it is never committed. Only `occo/` (published output), `CHANGELOG.md`, `CLAUDE.md`, and `.gitignore` are tracked in git.

---

## Critical Constraints

- **v0.0.1 is frozen.** The files under `src/v0.0.1/` represent the EC3 2026 paper submission version. Never modify them.
- **No `owl:imports`.** OCCO uses the MIREOT flat-file reuse pattern — external terms are re-declared locally with `rdfs:isDefinedBy`. This is consistent with SOSA, PROV-O, and SAREF4BLDG themselves.
- **No domain/range on foreign namespaces.** Adding `rdfs:domain` or `rdfs:range` to properties from external ontologies (SOSA, PROV-O, QUDT, etc.) constitutes axiom hijacking. Accept P11/P08 findings on external terms.
- **One-push strategy.** Complete all local work (WIDOCO, index.html, FOOPS, SPARQL CQ docs) before any push to GitHub Pages or PR to w3id.org.

---

## Toolchain

| Tool | Purpose |
|------|---------|
| Chowlk | Diagram-to-OWL conversion (draw.io → TTL) |
| OOPS! | OWL pitfall scanner — `https://oops.linkeddata.es` |
| FOOPS! | FAIR ontology scanner — `https://foops.linkeddata.es` |
| WIDOCO | HTML documentation generator from TTL |
| rdflib (Python) | Validation, triple counting, SPARQL testing |

---

## Sync Workflow

Edit the ontology in `src/v0.0.2/`. When ready to publish, copy to `occo/`:

```bash
BASE="$(git rev-parse --show-toplevel)"
cp "$BASE/src/v0.0.2/OCCO v0.0.2.ttl"                                 "$BASE/occo/occo.ttl"
cp "$BASE/src/v0.0.2/OCCO v0.0.2.rdf"                                 "$BASE/occo/occo.rdf"
cp "$BASE/src/v0.0.2/OCCO v0.0.2.ttl"                                 "$BASE/occo/releases/0.0.2/occo.ttl"
cp "$BASE/src/v0.0.2/OCCO v0.0.2.rdf"                                 "$BASE/occo/releases/0.0.2/occo.rdf"
cp "$BASE/src/v0.0.2/evaluation/oops/OCCO_OOPS_Evaluation_Report.md"  "$BASE/occo/evaluation/oops/"
cp "$BASE/src/v0.0.2/evaluation/oops/oops_response.xml"               "$BASE/occo/evaluation/oops/oops_response_v0.0.2.xml"
```

---

## Next Steps

See `NOTES.md` (local only, gitignored) for the current ordered next-steps checklist and status.
