# OCCO OOPS! Evaluation Report

**Ontology:** Occupant-Centric Control Ontology (OCCO)
**Namespace:** `https://w3id.org/occo#`
**Evaluation tool:** OOPS! (OntOlogy Pitfall Scanner) — https://oops.linkeddata.es
**Method:** OOPS! REST API (POST to `https://oops.linkeddata.es/rest`)
**Input format:** RDF/XML
**Versions evaluated:** v0.1.0 (baseline, 2026-03-26) and v0.1.1 (post-remediation, 2026-03-27)

---

## 1. Purpose

This report documents the quality evaluation of OCCO using the OOPS! automated pitfall scanner, covering both the initial baseline evaluation (v0.1.0) and the subsequent remediation cycle (v0.1.1). It is intended as reviewer-facing documentation for the EC3 2026 conference paper submission, where evidence of ontology quality evaluation and remediation was requested.

OOPS! checks ontologies against a catalogue of common modelling pitfalls derived from OWL 2 best-practice guidelines. Each detected pitfall carries a severity level:

| Severity | Meaning |
|----------|---------|
| **Critical** | Formal logical error; may cause incorrect inferences or reasoner failure |
| **Important** | Likely modelling error; may reduce interoperability or query correctness |
| **Minor** | Best-practice deviation; does not affect formal correctness but reduces usability |

---

## 2. v0.1.0 Baseline Results

**Version:** 0.1.0 · **Date:** 2026-03-26 · **Pitfalls scanned:** P02–P29

| Pitfall | Name | Severity | Count |
|---------|------|----------|-------|
| P19 | Defining multiple domains or ranges in properties | **Critical** | 1 |
| P10 | Missing disjointness | **Important** | 1 (ontology-level) |
| P11 | Missing domain or range in properties | **Important** | 11 |
| P04 | Creating unconnected ontology elements | Minor | 2 |
| P08 | Missing annotations | Minor | 67 |
| P13 | Inverse relationships not explicitly declared | Minor | 28 |
| P22 | Using different naming conventions | Minor | 2 |
| — | Suggestion: symmetric or transitive property | Suggestion | 1 |

**Totals:** 1 Critical · 2 Important · 4 Minor · 1 Suggestion

---

## 3. Remediation Actions — v0.1.0 → v0.1.1

The following changes were applied to the ontology to address v0.1.0 findings. All changes target specific OOPS! pitfalls; the rationale for each accepted or partially-accepted finding is documented in Section 5.

| Change | Pitfall Addressed |
|--------|-------------------|
| Remove multiple `rdfs:domain` axioms from `prov:wasAssociatedWith`; add single `rdfs:range prov:Agent` consistent with PROV-O specification | P19 (Critical) |
| Rename `occo:IncludesFeedback` → `occo:includesFeedback` | P22 (Minor) |
| Rename `occo:Overrides` → `occo:overrides` | P22 (Minor) |
| Add `rdfs:domain occo:PerformanceOutcome` to `occo:comfortScore` | P11 (Important) |
| Add `rdfs:domain occo:PerformanceOutcome` to `occo:meetsStandard` | P11 (Important) |
| Add `rdfs:domain occo:ControlStrategy` to `occo:strategyCategory` | P11 (Important) |
| Add `owl:AllDifferent` for `occo:MorningType`, `occo:EveningType`, `occo:IntermediateType` | P10 (Important) |
| Explicitly type all three Chronotype individuals as `occo:Chronotype` | P10 (Important) |
| Add `rdfs:comment` to all 26 OCCO-native classes and properties | P08 (Minor) |
| Remove isolated `time:TemporalEntity` class declaration | P04 (Minor) |
| Add `rdfs:isDefinedBy` to all ~30 re-declared external terms | P04 / MIREOT best practice |
| Update `owl:versionIRI` to `https://w3id.org/occo/0.1.1` and `owl:versionInfo` to `"0.1.1-dev"` | Metadata |

---

## 4. v0.1.1 Results

**Version:** 0.1.1-dev · **Date:** 2026-03-27 · **Triples:** 348

| Pitfall | Name | Severity | Count |
|---------|------|----------|-------|
| P10 | Missing disjointness | **Important** | 1 (ontology-level) |
| P11 | Missing domain or range in properties | **Important** | 9 |
| P08 | Missing annotations | Minor | 40 |
| P13 | Inverse relationships not explicitly declared | Minor | 28 |
| — | Suggestion: symmetric or transitive property | Suggestion | 1 |

**Totals:** 0 Critical · 2 Important · 2 Minor · 1 Suggestion

---

## 5. Before/After Comparison

| Pitfall | Severity | v0.1.0 | v0.1.1 | Outcome |
|---------|----------|--------|--------|---------|
| P19 | **Critical** | 1 | **0** | ✅ Resolved |
| P10 | Important | 1 | 1 | Partial — `owl:AllDifferent` added for Chronotype individuals; class disjointness deferred |
| P11 | Important | 11 | **9** | ✅ Reduced — 3 native properties fixed; 9 external accepted |
| P04 | Minor | 2 | **0** | ✅ Resolved |
| P08 | Minor | 67 | **40** | ✅ Reduced — 26 native elements annotated; 40 external accepted |
| P22 | Minor | 2 | **0** | ✅ Resolved |
| P13 | Minor | 28 | 28 | Accepted — see §6 |
| Suggestion | — | 1 | 1 | Declined — see §6 |

**Net change:** 1 Critical eliminated · 1 Important partially addressed · 2 Minor fully resolved · 1 Minor reduced · 1 Minor accepted

---

## 6. Detailed Findings

---

### P19 — Defining Multiple Domains or Ranges in Properties
**Severity: Critical** · **v0.1.0: 1 · v0.1.1: 0 · ✅ Resolved**

In v0.1.0, `prov:wasAssociatedWith` was declared with three separate `rdfs:domain` statements (`sosa:Actuation`, `occo:OverrideEvent`, `occo:VisualTask`). In OWL 2, multiple `rdfs:domain` axioms are interpreted as logical conjunction (AND), not disjunction (OR). This asserted that any subject of the property must simultaneously belong to all three classes — an unintended and likely unsatisfiable intersection.

**Fix:** All local `rdfs:domain` axioms were removed from `prov:wasAssociatedWith`. A single `rdfs:range prov:Agent` was added, consistent with the PROV-O specification for this property. A single range axiom does not trigger P19.

---

### P10 — Missing Disjointness
**Severity: Important** · **v0.1.0: 1 (ontology-level) · v0.1.1: 1 (ontology-level) · Partial fix**

OCCO v0.1.0 contained no `owl:disjointWith` or `owl:AllDifferent` axioms. Without disjointness constraints, a reasoner may treat distinct named individuals or classes as co-referential under the Open World Assumption.

**Partial fix:** An `owl:AllDifferent` block was added for the three `occo:Chronotype` named individuals:

```turtle
[] a owl:AllDifferent ;
    owl:members ( occo:MorningType occo:EveningType occo:IntermediateType ) .
```

This ensures a reasoner cannot conflate `MorningType`, `EveningType`, and `IntermediateType`.

**Deferred:** Comprehensive `owl:disjointWith` axioms between top-level domain classes (e.g., `occo:PerformanceOutcome`, `occo:ControlStrategy`, `ofo:Person`) require domain expert validation to confirm that the class boundaries are semantically correct and will not inadvertently render the ontology inconsistent. This is planned for v0.2.0.

---

### P11 — Missing Domain or Range in Properties
**Severity: Important** · **v0.1.0: 11 · v0.1.1: 9 · ✅ Reduced**

**Fixed (3 OCCO-native datatype properties):**

| Property | Domain Added |
|----------|-------------|
| `occo:comfortScore` | `occo:PerformanceOutcome` |
| `occo:meetsStandard` | `occo:PerformanceOutcome` |
| `occo:strategyCategory` | `occo:ControlStrategy` |

**Accepted (9 external properties):** The remaining 9 affected properties are all from external ontologies (Dublin Core, OFO, PROV-O, SOSA, QUDT). Their domain definitions exist in their respective source specifications. Re-declaring domain/range for properties in foreign namespaces would constitute axiom hijacking. These are accepted under the MIREOT flat-file reuse pattern.

---

### P04 — Creating Unconnected Ontology Elements
**Severity: Minor** · **v0.1.0: 2 · v0.1.1: 0 · ✅ Resolved**

In v0.1.0, two classes appeared with no property domain or range connection to the rest of the graph: `prov:Agent` and `time:TemporalEntity`. Both were external root superclasses re-declared as anchors for the local class hierarchy.

**Fix:** `time:TemporalEntity` was removed — it was an intermediate superclass with no direct property connections in OCCO; `time:Instant` and `time:Interval` retain standalone declarations as they are directly used. For `prov:Agent`, the property graph was extended: `rdfs:range prov:Agent` was added to `prov:wasAssociatedWith` (consistent with the PROV-O specification), connecting `prov:Agent` to the property graph and resolving the P04 finding. The `prov:SoftwareAgent rdfs:subClassOf prov:Agent` axiom is retained to preserve the PROV-O class hierarchy for consumers loading only `occo.ttl` without `owl:imports`.

---

### P08 — Missing Annotations
**Severity: Minor** · **v0.1.0: 67 · v0.1.1: 40 · ✅ Reduced**

**Fixed (26 OCCO-native elements):** `rdfs:comment` descriptions were added to all native classes and properties:

- **Classes (11):** `occo:Controller`, `occo:VisualTask`, `occo:Preference`, `occo:PerformanceOutcome`, `occo:ControlStrategy`, `occo:CCT`, `occo:GlareIndex`, `occo:Illuminance`, `occo:OccupancyStatus`, `occo:Chronotype`, `occo:OverrideEvent`
- **Object Properties (12):** `occo:hasPreference`, `occo:hasChronotype`, `occo:preferredIlluminance`, `occo:preferredCCT`, `occo:usesStrategy`, `occo:appliesToSpace`, `occo:assessedAgainst`, `occo:includesFeedback`, `occo:hasBaseline`, `occo:hasEnergyConsumption`, `occo:overrides`, `occo:forTask`
- **Datatype Properties (3):** `occo:comfortScore`, `occo:meetsStandard`, `occo:strategyCategory`

**Accepted (40 external elements):** The 40 remaining unannotated elements are from external ontologies (SOSA, PROV-O, QUDT, OWL-Time, SAREF4BLDG, OFO, Dublin Core) re-declared in the flat file. Their annotations are the responsibility of their source ontologies.

---

### P13 — Inverse Relationships Not Explicitly Declared
**Severity: Minor** · **v0.1.0: 28 · v0.1.1: 28 · Accepted**

No `owl:inverseOf` axioms are declared. Inverse declarations are not required by the competency questions defined in the ORSD. Properties from external ontologies (SOSA, PROV-O, OWL-Time) declare inverses where semantically appropriate in their source specifications. Accepted.

---

### P22 — Using Different Naming Conventions
**Severity: Minor** · **v0.1.0: 2 · v0.1.1: 0 · ✅ Resolved**

Two object properties were found using PascalCase instead of the lowerCamelCase convention used throughout OCCO:

| Property | v0.1.0 | v0.1.1 |
|----------|--------|--------|
| `occo:IncludesFeedback` | PascalCase | Renamed to `occo:includesFeedback` |
| `occo:Overrides` | PascalCase | Renamed to `occo:overrides` |

Both renames were applied in the source Chowlk diagram prior to re-conversion. P22 fully resolved.

---

### Suggestion — Symmetric or Transitive Property
**v0.1.0: 1 · v0.1.1: 1 · Declined**

OOPS! suggests `occo:hasBaseline` may be symmetric or transitive, as its domain and range are both `occo:PerformanceOutcome`. The property is neither: it expresses a directional reference — a performance outcome is compared *against* a designated baseline, but not vice versa. The `rdfs:comment` added in v0.1.1 explicitly documents this directionality. Declined.

---

## 7. Notes on External Term Reuse (MIREOT)

OCCO re-declares external terms locally using the MIREOT (Minimum Information to Reference an External Ontology Term) pattern. Each re-declared term carries `rdfs:isDefinedBy` pointing to its source ontology, providing source traceability without `owl:imports` transitive dependency chains. This approach is consistent with SOSA, PROV-O, and SAREF4BLDG themselves, none of which use `owl:imports`. OOPS! P08 and P11 findings on external terms are inherent to this pattern and are accepted throughout this report.

---

## 8. Notes on OOPS! Coverage

The implemented pitfall checks cover P02–P29. Pitfalls P30–P41 remain catalogued but are not yet implemented in the scanner. OCCO's flat-file reuse pattern would likely be flagged by P40 (Namespace Hijacking) if implemented. This is a known architectural decision made to ensure a self-contained standalone OWL file during early development, consistent with MIREOT best practice.

---

*OOPS! evaluations performed via REST API. Raw scanner responses: `oops_response_v0.1.0.xml` and `oops_response_v0.1.1.xml`.*
