### About

This changelog records all notable updates and revisions to the **WRITE ontology**, in line with principles of **FAIR data management**.  
Each entry reflects a public release of the ontology, documenting any changes.

Versioning follows the principles of [Semantic Versioning](https://semver.org/).    
This document ensures that all modifications are traceable and citable across releases.

---

## [v2.0.0] – 2026-10-28
**Major update**

- **Naming conventions**: Standardised property names using camelCase and improved naming consistency across classes and properties.
- **New object properties**: Introduced new relationships, including inverse properties, to improve the representation of connections between entities.
- **Improved semantic modelling**: Refined domain and range definitions and introduced additional OWL constructs, including symmetric and disjoint properties.
- **Wikidata integration**: Updated Wikidata property references to improve consistency and interoperability.
- **Documentation**: Expanded property descriptions and added SKOS scope notes to clarify the intended use of ontology terms.
- **Namespace update**: Standardised ontology URIs and updated the version IRI.

---

## [v1.0.0] – 2025-02-05
**Major update (current version)**

- Transformed the initial data model into a **fully fledged OWL ontology**
- Added a few new **classes** and numerous new **properties** to expand the ontology coverage    
- Deleted unnecessary properties to avoid redundancy    
- Defined **domain and range** for all object and data properties    
- Revised and updated all **descriptions and annotations** for clarity and accuracy    
- Officially registered the ontology with **w3id**, providing persistent and resolvable IRIs    
- Created a **human-readable version** of the ontology using **pyLODE**    
- OWL files updated and provided in **Turtle (`.ttl`) format**

  ---

## [v0.1.0] – 2020-04-09
**Core draft (data model)**

The core draft version of the WRITE data model was created by the former collaborator, as a structured RDF-based data model.  
It included preliminary concepts and properties to capture key entities in the domain, with minimum descriptions and without domain / range declarations.  
Turtle files were provided for basic semantic interoperability.  

Note: the base IRI http://w3id.org/write/ontology/ was included in this draft as a provisional placeholder before the namespace was registered and resolvable. As of the first release (v1.0.0, 2025-02-05), the namespace is registered and resolvable.

