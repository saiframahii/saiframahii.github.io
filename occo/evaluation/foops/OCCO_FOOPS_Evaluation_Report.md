# OCCO FOOPS! Evaluation Report

**Ontology:** Occupant-Centric Control Ontology (OCCO)
**Namespace:** `https://w3id.org/occo#`
**Evaluation tool:** FOOPS! v0.3.1 (FAIR Ontology Pitfall Scanner) — https://foops.linkeddata.es
**Input (pre-publication):** Local file `OCCO v0.0.2.ttl`, run via Docker (eclipse-temurin:11)
**Input (post-publication):** `https://w3id.org/occo` — *to be run after w3id.org PR is merged*
**Version evaluated:** v0.0.2-dev (365 triples)
**Date of pre-publication pass:** 2026-03-29

---

## 1. Purpose

This report documents the FAIRness evaluation of OCCO using the FOOPS! scanner. FOOPS assesses ontologies against the FAIR principles (Findability, Accessibility, Interoperability, Reusability) as applied to ontology engineering. It complements the OOPS! structural quality evaluation (see `OCCO_OOPS_Evaluation_Report.md`).

FOOPS is run in two passes:

1. **Pre-publication pass** (this document, Section 3) — run locally against the TTL file. Catches R/I (Reusability/Interoperability) issues before publishing. F/A checks are expected to be infrastructure-dependent and may report warnings until the w3id.org redirect is live.
2. **Post-publication pass** (Section 5) — run against the live URI `https://w3id.org/occo` after the w3id.org PR is merged. Validates F/A checks.

---

## 2. Pre-evaluation Metadata Checklist

The following metadata properties were added to OCCO v0.0.2 in preparation for FOOPS:

| Metadata | Property | Value |
|----------|----------|-------|
| Title | `dcterms:title` | "Occupant-Centric Control Ontology (OCCO)" |
| Description | `dcterms:description` | present |
| Version IRI | `owl:versionIRI` | `https://w3id.org/occo/0.0.2` |
| Version string | `owl:versionInfo` | `"0.0.2-dev"` |
| Creator | `dcterms:creator` | Saif Alramahi; Mohammad Mayouf; Elham Del Zendeh; Khalid Ismail |
| Publisher | `dcterms:publisher` | Birmingham City University |
| Date issued | `dcterms:issued` | `"2026-03-29"^^xsd:date` |
| License | `dcterms:license` | CC BY 4.0 |
| Namespace prefix | `vann:preferredNamespacePrefix` | `"occo"` |
| Namespace URI | `vann:preferredNamespaceUri` | `https://w3id.org/occo#` |
| Bibliographic citation | `dcterms:bibliographicCitation` | EC3 2026 paper (submitted) |
| Source repository | `dcterms:source` | GitHub Pages repo |
| Ontology status | `bibo:status` | "Ontology Specification Draft" |
| Persistent URI | w3id.org redirect | `https://w3id.org/occo` → GitHub Pages |
| Labels | `rdfs:label` | All 26 native terms + re-declared external terms |
| Definitions | `rdfs:comment` | All 26 native OCCO terms |
| Source traceability | `rdfs:isDefinedBy` | All re-declared external terms |

---

## 3. Pre-publication Results (2026-03-29)

**Overall FOOPS score: 0.978 (97.8%)** — 14/15 checks passed

### Score by FAIR Dimension

| Dimension | Passed | Total | Score |
|-----------|--------|-------|-------|
| Findable | 4 | 4 | 100% |
| Accessible | — | — | n/a (no dedicated checks in v0.3.1) |
| Interoperable | 3 | 3 | 100% |
| Reusable | 7 | 8 | 87.5% |
| **Total** | **14** | **15** | **97.8%** |

### Detailed Check Results

| Check | Title | Result |
|-------|-------|--------|
| PURL1 | Ontology has a persistent URL | ✅ Pass |
| RDF1 | Ontology is available in RDF | ✅ Pass |
| OM1 | Ontology minimum metadata is declared | ✅ Pass |
| OM2 | Ontology declares recommended metadata | ✅ Pass |
| OM3 | Ontology declares detailed metadata | ❌ Fail |
| OM4.1 | Ontology has a license available | ✅ Pass |
| OM4.2 | Ontology license is resolvable | ✅ Pass |
| OM5.1 | Ontology declares basic provenance metadata | ✅ Pass |
| OM5.2 | Ontology declares detailed provenance metadata | ✅ Pass |
| FIND1 | Ontology prefix is declared | ✅ Pass |
| VOC1 | Ontology reuses existing vocabularies for metadata | ✅ Pass |
| VOC2 | Ontology imports/reuses well-established vocabularies | ✅ Pass |
| VOC3 | All terms have labels | ✅ Pass |
| VOC4 | All terms have definitions | ✅ Pass |
| VER1 | Version IRI is declared | ✅ Pass |

### Failure Detail

**OM3 — Ontology declares detailed metadata** ❌

- **Missing (required):** `doi`, `logo`
- **Missing (optional):** previous version URI, backwards compatibility statement
- **Decision:** Not fixable pre-publication. DOI requires a published paper (paper submitted to EC3 2026, DOI pending). A logo image is cosmetic and not needed for initial publication. These will be addressed if/when DOI is assigned and in a future version.

---

## 4. Remediation Actions Taken

The following issues were identified and resolved during the pre-publication pass:

| Issue | Check | Action Taken |
|-------|-------|-------------|
| Missing `dcterms:bibliographicCitation` | OM2 | Added to ontology header with EC3 2026 submitted paper reference |
| Missing `dcterms:publisher` in header | OM3, OM5.2 | Added `"Birmingham City University"` to ontology header |
| Missing `bibo:status` | OM3 | Added `"Ontology Specification Draft"` + MIREOT declaration |
| Missing `dcterms:source` | OM3 | Added GitHub Pages repo URI + MIREOT declaration |
| `dcterms:title` punning (AnnotationProperty + DatatypeProperty) | OWLAPI warning | Fixed — removed duplicate DatatypeProperty declaration |

---

## 5. Post-publication Results

*To be completed after the w3id.org PR is merged and `https://w3id.org/occo` is live.*

Run command:
```bash
MSYS_NO_PATHCONV=1 docker run --rm \
  -v "C:/Users/sbram/AppData/Local/Temp/foops_run:/work" \
  eclipse-temurin:11 \
  java -jar /work/foops.jar -ontURI https://w3id.org/occo -out /work/out_postpub
```

| Check | Title | Result |
|-------|-------|--------|
| *(all 15 checks)* | — | *pending* |

**Score:** *pending*

---

*Pre-publication pass run locally on 2026-03-29 using FOOPS! v0.3.1 JAR via Docker (eclipse-temurin:11).*
