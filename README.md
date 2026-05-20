# RDM-Maturity-Model-Assessment-Toolkit-
RDM maturity model for research data management. Includes Excel-based assessment, Python scripts for ontology generation, OWL/SWRL reasoning for automated maturity inference, and SPARQL verification across five test projects


# RDM Maturity Model — Research Data Management

This repository provides a comprehensive framework for assessing and verifying
the maturity of research data management (FDM) practices across five process
areas: **Planning, Collection, Analysis & Synthesis, Archiving, and Access**.

---

## Maturity Model

The model defines five maturity levels per process area, each characterized by
specific goals and practices. The full model is documented in a structured Excel
table covering all process areas, goals, and practices across all five maturity
levels. It serves as the conceptual foundation for both the self-assessment tool
and the ontology.

## Self-Assessment Tool

An Excel-based tool that allows research projects to assess their current FDM
maturity level across all process areas. Users document which practices are
applied and derive their maturity level per process area.

## Ontology

The maturity model is formally represented as an OWL ontology. SWRL rules encode
the cumulative maturity logic: a project reaches a maturity level if and only if
all practices of that level and all preceding levels are fulfilled.

## Python Script

Python scripts automate the generation of project-specific OWL ontology instances
and the merging of multiple project ontologies into a single knowledge base.

 
### Verification Files

The ontology-based maturity inference is verified across five test projects using
a SPARQL query on the merged inferred ontology, producing a Soll-Ist comparison
table matching the manual assessment results.
 
| File                              | Description                                                                                     |
|-----------------------------------|-------------------------------------------------------------------------------------------------|
| `Projekt1.owl` – `Projekt5.owl`   | Individual OWL ontologies per project, each with project-specific `wendenPraktikAn` assertions |
| `Merged_AlleProjekte.owl`         | All five project individuals combined in a single shared knowledge base; input for the reasoner |
| `Merged_AlleProjekte_Inferiert.owl` | Inferred ontology exported after running the HermiT reasoner in Protégé; contains all `erzieltReifegrad` triples as asserted facts |
| `SPARQL.txt`                      | SPARQL query executed on the inferred ontology to retrieve the achieved maturity level per project and process area; output corresponds to the Soll-Ist table |
