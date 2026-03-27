# Changelog — Occupant-Centric Control Ontology (OCCO)

All notable changes to OCCO are documented here.

---

## [0.0.2] — 2026-03-27

### Quality Evaluation
- Evaluated against OOPS! pitfall scanner (P02–P29); full report at `evaluation/oops/OCCO_OOPS_Evaluation_Report.md`
- Eliminated the sole Critical finding from v0.0.1; reduced Important and Minor findings

### Fixed
- **P19 (Critical)** — Removed multiple `rdfs:domain` axioms from `prov:wasAssociatedWith`; added single `rdfs:range prov:Agent` consistent with the PROV-O specification
- **P22 (Minor)** — Renamed `occo:IncludesFeedback` → `occo:includesFeedback` and `occo:Overrides` → `occo:overrides` to restore lowerCamelCase convention
- **P04 (Minor)** — Removed isolated `time:TemporalEntity` class; connected `prov:Agent` to the property graph via `prov:wasAssociatedWith rdfs:range prov:Agent`

### Improved
- **P11 (Important)** — Added `rdfs:domain` to three native datatype properties: `occo:comfortScore`, `occo:meetsStandard`, `occo:strategyCategory`; 9 external-ontology properties accepted
- **P10 (Important)** — Added `owl:AllDifferent` for the three `occo:Chronotype` named individuals; full class disjointness deferred to v0.0.3 pending domain expert validation
- **P08 (Minor)** — Added `rdfs:comment` annotations to all 26 OCCO-native classes and properties; 40 external-ontology elements accepted

### Accepted (no change)
- **P13 (Minor)** — Inverse relationships not declared; not required by competency questions
- **Suggestion** — `occo:hasBaseline` is directional by design; symmetry/transitivity declined

### Metadata
- Added `rdfs:isDefinedBy` to all ~30 re-declared external terms (MIREOT pattern)
- Updated `owl:versionIRI` to `https://w3id.org/occo/0.0.2`
- Updated `owl:versionInfo` to `"0.0.2-dev"`

---

## [0.0.1] — 2026-03-26

Initial release. Generated from Chowlk diagram and submitted with the EC3 2026 conference paper.

### Known issues at time of release (addressed in v0.0.2)
- P19 Critical: multiple `rdfs:domain` on `prov:wasAssociatedWith` interpreted as class intersection
- P11 Important: three native datatype properties missing `rdfs:domain`
- P22 Minor: `occo:IncludesFeedback` and `occo:Overrides` used PascalCase
- P08 Minor: no `rdfs:comment` on any native element
- P04 Minor: `prov:Agent` and `time:TemporalEntity` unconnected from property graph
