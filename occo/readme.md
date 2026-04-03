# Occupant-Centric Control Ontology (OCCO)

**Namespace:** `https://w3id.org/occo#`

**Persistent URI:** `https://w3id.org/occo`

**Version:** 0.1.1-dev

**License:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

**Status:** Ontology Specification Draft — ongoing doctoral research

---

## Overview

OCCO is an OWL ontology providing a semantic framework for occupant-centric control (OCC) in smart buildings. OCC embeds real-time occupant information — presence, preferences, and activity — into building control logic to jointly optimise comfort and energy efficiency. Lighting systems are the primary application domain in this version: they carry significant energy loads and directly shape occupant visual comfort. OCCO models the relationships between occupants, their preferences and comfort feedback, environmental observations, control strategies, and actuation events, unifying subjective occupant feedback with objective sensor data in a single interoperable model.

OCCO is developed as part of PhD research at Birmingham City University following the LOT (Linked Open Terms) methodology, with competency questions derived from a systematic review of 41 OCC studies. It reuses established vocabularies including SOSA/SSN, SAREF4BLDG, PROV-O, QUDT, OWL-Time, and Dublin Core via the MIREOT flat-file pattern (no `owl:imports`).

---

## Documentation

Full ontology documentation (WIDOCO-generated): [index-en.html](index-en.html)

Interactive visualisation (WebVOWL): [webvowl/index.html](webvowl/index.html)

---

## Ontology Files

| Format | File |
|--------|------|
| Turtle | [occo.ttl](occo.ttl) |
| RDF/XML | [occo.rdf](occo.rdf) |
| OWL/XML | [ontology.owl](ontology.owl) |
| N-Triples | [ontology.nt](ontology.nt) |
| JSON-LD | [ontology.jsonld](ontology.jsonld) |

Content negotiation is supported — dereference `https://w3id.org/occo` with the appropriate `Accept` header to receive your preferred format.

---

## Evaluation

| Tool | Report |
|------|--------|
| OOPS! (structural quality) | [evaluation/oops/OCCO_OOPS_Evaluation_Report.md](evaluation/oops/OCCO_OOPS_Evaluation_Report.md) |
| FOOPS! (FAIR compliance, 88.2%) | [evaluation/foops/OCCO_FOOPS_Evaluation_Report.md](evaluation/foops/OCCO_FOOPS_Evaluation_Report.md) |
| SPARQL competency questions (CQ1–CQ10) | [evaluation/sparql/](evaluation/sparql/) |

---

## Citation

> Alramahi, S., Mayouf, M., Del Zendeh, E., & Ismail, K. (2026). *Towards a Semantic Ontology for Occupant-Centric Building Control*. Submitted to EC3 2026 — 12th European Conference on Construction IT.

---

## Contact

**Saif Alramahi**
Birmingham City University
saif.alramahi@mail.bcu.ac.uk
GitHub: [@saiframahii](https://github.com/saiframahii)
