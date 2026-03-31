# Changelog — Occupant-Centric Control Ontology (OCCO)

All notable changes to OCCO are documented here.

---

## [0.0.2] — 2026-03-29

### Publication Infrastructure
- Published WIDOCO-generated HTML documentation at `occo/index-en.html` with all seven sections (abstract, introduction, overview, description, crossref, ns, references)
- Added WebVOWL interactive visualisation at `occo/webvowl/`
- Published multi-format serialisations: Turtle (`occo.ttl`), RDF/XML (`occo.rdf`), OWL/XML (`ontology.owl`), N-Triples (`ontology.nt`), JSON-LD (`ontology.jsonld`)
- Added `.htaccess` content negotiation (HTML / Turtle / RDF+XML / N-Triples / JSON-LD) for `https://w3id.org/occo`
- Added PROV-O provenance document (`provenance/provenance-en.ttl` and `provenance/provenance-en.html`)

### SPARQL Competency Question Evaluation
- Tested all 10 competency questions (CQ-01–CQ-10) using rdflib 7.6.0 (SPARQL 1.1); all queries return expected results against synthetic ABox data
- Published query files (`.rq`), synthetic instance data (`.ttl`), and result tables at `evaluation/sparql/` — one subdirectory per CQ

### FAIR Evaluation (FOOPS!)
- Post-publication score: **88.2% (19 of 22 checks passed)** — evaluated against live URI `https://w3id.org/occo` on 2026-03-31 — full report at `evaluation/foops/OCCO_FOOPS_Evaluation_Report.md`
- Failures: OM3 (`doi`/`logo` not yet available), FIND2 (OBO prefix.cc namespace collision — not fixable), FIND3/FIND_3_BIS (LOV registration pending)
- Expected score after LOV registration: ~94.4%

### Structural Evaluation (OOPS! pitfall scanner)
- Evaluated against OOPS! (P02–P29); full report at `evaluation/oops/OCCO_OOPS_Evaluation_Report.md`
- Eliminated the sole Critical finding from v0.0.1; reduced Important and Minor findings

### Fixed
- **P19 (Critical)** — Removed multiple `rdfs:domain` axioms from `prov:wasAssociatedWith`; added single `rdfs:range prov:Agent` consistent with PROV-O
- **P22 (Minor)** — Renamed `occo:IncludesFeedback` → `occo:includesFeedback` and `occo:Overrides` → `occo:overrides` to restore lowerCamelCase convention
- **P04 (Minor)** — Removed isolated `time:TemporalEntity` class; connected `prov:Agent` to the property graph via `prov:wasAssociatedWith rdfs:range prov:Agent`
- **FOOPS OM2** — Added `dcterms:bibliographicCitation` (EC3 2026 submitted paper)
- **FOOPS OM3/OM5.2** — Added `dcterms:publisher` (`"Birmingham City University"`) to ontology header
- **FOOPS OM3** — Added `bibo:status` (`"Ontology Specification Draft"`)
- **FOOPS OM3** — Added `dcterms:source` (GitHub Pages repo URI)
- **OWLAPI warning** — Fixed `dcterms:title` punning (removed duplicate DatatypeProperty declaration)

### Improved
- **P11 (Important)** — Added `rdfs:domain` to three native datatype properties: `occo:comfortScore`, `occo:meetsStandard`, `occo:strategyCategory`; 9 external-ontology properties accepted (no domain/range axiom hijacking)
- **P10 (Important)** — Added `owl:AllDifferent` for the three `occo:Chronotype` named individuals; full class disjointness deferred to v0.0.3
- **P08 (Minor)** — Added `rdfs:comment` annotations to all 26 OCCO-native classes and properties; 40 external-ontology elements accepted

### Accepted (no change)
- **P13 (Minor)** — Inverse relationships not declared; not required by competency questions
- **Suggestion** — `occo:hasBaseline` is directional by design; symmetry/transitivity declined

### Metadata
- Added `rdfs:isDefinedBy` to all ~30 re-declared external terms (MIREOT pattern)
- Updated `owl:versionIRI` to `https://w3id.org/occo/0.0.2`
- Updated `owl:versionInfo` to `"0.0.2-dev"`
- Added `rdfs:label` to all 26 native terms and re-declared external terms

---

## [0.0.1] — 2026-03-26

Initial release. Generated from Chowlk diagram and submitted with the EC3 2026 conference paper.

### Known issues at time of release (addressed in v0.0.2)
- P19 Critical: multiple `rdfs:domain` on `prov:wasAssociatedWith` interpreted as class intersection
- P11 Important: three native datatype properties missing `rdfs:domain`
- P22 Minor: `occo:IncludesFeedback` and `occo:Overrides` used PascalCase
- P08 Minor: no `rdfs:comment` on any native element
- P04 Minor: `prov:Agent` and `time:TemporalEntity` unconnected from property graph
