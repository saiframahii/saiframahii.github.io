# OCCO FOOPS! Evaluation Report

**Ontology:** Occupant-Centric Control Ontology (OCCO)
**Namespace:** `https://w3id.org/occo#`
**Evaluation tool:** FOOPS! (FAIR Ontology Pitfall Scanner) — https://foops.linkeddata.es
**Input:** `https://w3id.org/occo` (live persistent URI via w3id.org)
**Version evaluated:** v0.1.1-dev
**Date of evaluation:** 2026-03-31

---

## 1. Purpose

This report documents the FAIRness evaluation of OCCO using the FOOPS! scanner, run against the live published URI `https://w3id.org/occo`. FOOPS assesses ontologies against the FAIR principles (Findability, Accessibility, Interoperability, Reusability) as applied to ontology engineering.

The evaluation was conducted post-publication, after the w3id.org persistent redirect was confirmed live and GitHub Pages was serving all serialisations (RDF/XML, TTL, HTML). FOOPS resolves the ontology via `application/rdf+xml` content negotiation, and all 22 checks were run against the live URI.

---

## 2. Metadata Declared in OCCO v0.1.1

The following metadata properties are present in the published ontology:

| Metadata | Property | Value |
|----------|----------|-------|
| Title | `dcterms:title` | "Occupant-Centric Control Ontology (OCCO)" |
| Description | `dcterms:description` | present |
| Version IRI | `owl:versionIRI` | `https://w3id.org/occo/0.1.1` |
| Version string | `owl:versionInfo` | `"0.1.1-dev"` |
| Creator | `dcterms:creator` | Saif Alramahi; Mohammad Mayouf; Elham Del Zendeh; Khalid Ismail |
| Publisher | `dcterms:publisher` | Birmingham City University |
| Date created | `dcterms:created` | `"2025-09-24"^^xsd:date` |
| Date issued | `dcterms:issued` | `"2026-03-29"^^xsd:date` |
| Date modified | `dcterms:modified` | `"2026-03-29"^^xsd:date` |
| License | `dcterms:license` | CC BY 4.0 |
| Namespace prefix | `vann:preferredNamespacePrefix` | `"occo"` |
| Namespace URI | `vann:preferredNamespaceUri` | `https://w3id.org/occo#` |
| Bibliographic citation | `dcterms:bibliographicCitation` | EC3 2026 paper (submitted) |
| Source repository | `dcterms:source` | GitHub Pages repo |
| Ontology status | `bibo:status` | "Ontology Specification Draft" |
| Persistent URI | w3id.org redirect | `https://w3id.org/occo` → GitHub Pages |
| Labels | `rdfs:label` | All 26 native OCCO terms |
| Definitions | `rdfs:comment` | All 26 native OCCO terms |
| Source traceability | `rdfs:isDefinedBy` | All re-declared external terms |

---

## 3. Results

**Overall FOOPS score: 0.882 (88.2%)** — 22 checks run

### Score by FAIR Dimension

| Dimension | Checks | Failures | Notes |
|-----------|--------|----------|-------|
| Findable | PURL1, URI1, URI2, VER1, VER2, OM1, FIND1, FIND2, FIND3 | FIND2, FIND3 | See §4 |
| Accessible | CN1, HTTP1, FIND_3_BIS | FIND_3_BIS | Tied to LOV registration |
| Interoperable | RDF1, VOC1, VOC2 | — | 100% |
| Reusable | DOC1, OM2, OM3, OM4.1, OM4.2, OM5.1, OM5.2, VOC3, VOC4 | OM3 (partial) | See §4 |

### Detailed Check Results

| Check | Title | Result | Detail |
|-------|-------|--------|--------|
| PURL1 | Ontology has a persistent URL | ✅ Pass | w3id.org URI scheme confirmed |
| URI1 | Ontology URI is resolvable | ✅ Pass | Resolves in application/rdf+xml |
| URI2 | Consistent ontology IDs are employed | ✅ Pass | Ontology URI = ontology ID |
| CN1 | Ontology has content negotiation for RDF | ✅ Pass | HTML and RDF both available |
| HTTP1 | Ontology uses an open protocol | ✅ Pass | HTTPS |
| RDF1 | Ontology is available in RDF | ✅ Pass | Valid RDF serialisation loaded |
| DOC1 | Ontology has HTML documentation | ✅ Pass | WIDOCO-generated HTML served |
| OM1 | Ontology minimum metadata is declared | ✅ Pass | All 6/6 minimum fields found |
| OM2 | Ontology declares recommended metadata | ✅ Pass | All 4/4 required fields found (contributor: optional, not present) |
| OM3 | Ontology declares detailed metadata | ❌ Fail | 4/6 — missing: doi, logo |
| OM4.1 | Ontology has a license available | ✅ Pass | CC BY 4.0 |
| OM4.2 | Ontology license is resolvable | ✅ Pass | License URI resolves |
| OM5.1 | Ontology declares basic provenance metadata | ✅ Pass | creator + creation date found |
| OM5.2 | Ontology declares detailed provenance metadata | ✅ Pass | issued date + publisher found |
| FIND1 | Ontology prefix is declared | ✅ Pass | `occo` prefix declared |
| FIND2 | Ontology prefix found in prefix.cc or LOV | ❌ Fail | `occo` exists in prefix.cc but maps to a different OBO ontology (`http://purl.obolibrary.org/obo/OCCO_`) — namespace mismatch |
| FIND3 | Ontology found in community registry (LOV) | ❌ Fail | Not yet registered in LOV |
| FIND_3_BIS | Ontology metadata accessible even when ontology is not | ❌ Fail | Dependent on LOV registration |
| VER1 | A version IRI is declared | ✅ Pass | `owl:versionIRI` + `owl:versionInfo` both present |
| VER2 | Ontology version IRI resolves | ✅ Pass | `https://w3id.org/occo/0.1.1` resolves |
| VOC1 | Ontology reuses existing vocabularies for metadata | ✅ Pass | dcterms, bibo, vann, rdfs, owl, mod |
| VOC2 | Ontology imports/reuses well-established vocabularies | ✅ Pass | SOSA, PROV-O, QUDT, OWL-Time, OFO, SAREF4BLDG |
| VOC3 | All terms have labels | ✅ Pass | 26/26 terms labelled |
| VOC4 | All terms have definitions | ✅ Pass | 26/26 terms defined |

---

## 4. Failure Analysis

### OM3 — Ontology declares detailed metadata ❌ (4/6)

**Missing (required):** `doi`, `logo`

- **DOI:** Requires a published paper with an assigned DOI. The associated paper (Alramahi et al.) has been submitted to EC3 2026 but a DOI has not yet been assigned. This will be added to the ontology header once available.
- **Logo:** Cosmetic metadata; not planned for v0.1.1.

**Missing (optional, no penalty):** previous version URI, backwards compatibility statement. Not applicable — v0.1.1 is the first published release.

### FIND2 — Prefix found with incorrect namespace ❌

The prefix `occo` is registered in prefix.cc but maps to a different ontology: `http://purl.obolibrary.org/obo/OCCO_` (an OBO ontology unrelated to OCCO). This is a name collision and is not fixable without coordination with the OBO community. Registration of OCCO in LOV (see FIND3) would allow FOOPS to resolve the correct namespace via that registry.

### FIND3 / FIND_3_BIS — Not in LOV ❌

OCCO has not yet been submitted to the Linked Open Vocabularies (LOV) registry. LOV registration is planned as a post-v0.1.1 task. Once registered, both FIND3 and FIND_3_BIS will pass, and the overall score will increase to approximately 94.4%.

---

## 5. Known Limitations

- The FIND2 failure reflects a pre-existing prefix.cc name collision with an OBO ontology, not an error in OCCO's metadata.
- FIND3 and FIND_3_BIS are expected to fail for any newly published ontology not yet registered in LOV. These are infrastructure gaps, not design issues.
- OM3 will be partially resolved once the EC3 2026 DOI is assigned.

---

*Evaluation run on 2026-03-31 using FOOPS! against the live URI `https://w3id.org/occo`. FOOPS resolves the ontology via `application/rdf+xml` content negotiation.*
