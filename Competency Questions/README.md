### WRITE Competency Questions and SPARQL Queries 

This page documents the 27 competency questions (CQs) developed for WenDAng and their corresponding SPARQL queries. They are organised into three groups and support the analysis of what can be retrieved from the WRITE RDF knowledge graph using the WRITE Ontology (v2.0.0).

#### How to use the queries

The following SPARQL queries are provided as templates for exploring the WRITE knowledge graph.

To execute them:

1. Download the RDF dataset from the [WRITE data repository](https://github.com/wendang-project/data).
2. Load the Turtle (.ttl) file into a SPARQL-compatible environment, such as Apache Jena Fuseki.
3. Replace the placeholders with the URIs of the resources you wish to investigate:
   - `<ARTWORK_URI>` — URI of a selected artwork.
   - `<UNIT_URI>` — URI of a selected Calli-Writing unit.
   - `<PERSON_URI>` — URI of a selected artist.

## Contents

- [Group 1 — Artistic Analysis](#group-1--artistic-analysis)
- [Group 2 — Linguistic/Textual Analysis](#group-2--linguistictextual-analysis)
- [Group 3 — Socio-Political-Economic Analysis](#group-3--socio-political-economic-analysis)

## Group 1 — Artistic Analysis

### CQ 1.1 — What is the artwork type?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?typeLabel
WHERE {
  <ARTWORK_URI> write:hasVisualArtworkType ?type .
  ?type rdfs:label ?typeLabel .
}
```
**Note:** Depending on the artwork category, the following properties can be used:
- `write:hasVisualArtworkType` — Visual Arts
- `write:hasPerformingArtworkType` — Performing Arts
- `write:hasDecorativeArtworkType` — Decorative and Applied Arts
- `write:hasGraffitiType` — Graffiti

### CQ 1.2 — Who created the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?creator
WHERE {
  <ARTWORK_URI> wdt:P170 ?creator .
}
```

### CQ 1.3 — When was the artwork created?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?date
WHERE {
  <ARTWORK_URI> wdt:P571 ?date .
}
```
**Note:** Depending on the artwork category, the following properties can be used:
- `wdt:P571` — Date of creation (Visual Arts, Graffiti, Decorative and Applied Arts)
- `wdt:P585` — Date (Performing Arts)

### CQ 1.4 — What materials and tools were used to create the artwork?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?materialLabel ?toolLabel
WHERE {
  OPTIONAL {
    <ARTWORK_URI> wdt:P186 ?material .
    ?material rdfs:label ?materialLabel .
  }

  OPTIONAL {
    <ARTWORK_URI> write:madeUsingTool ?tool .
    ?tool rdfs:label ?toolLabel .
  }
}
```

### CQ 1.5 — What are the dimensions of the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT ?height ?width
WHERE {
  OPTIONAL { <ARTWORK_URI> wdt:P2048 ?height . }
  OPTIONAL { <ARTWORK_URI> wdt:P2049 ?width . }
}
```

### CQ 1.6 — What colours are present in the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?colourLabel
WHERE {
  <ARTWORK_URI> wdt:P462 ?colour .
  ?colour rdfs:label ?colourLabel .
}
```

### CQ 1.7 — Does the artwork contain a seal, a colophon, both, or neither?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?seal ?colophon
       (IF(COALESCE(?seal, false) && COALESCE(?colophon, false), "both",
         IF(COALESCE(?seal, false), "seal only",
           IF(COALESCE(?colophon, false), "colophon only", "neither"))) AS ?status)
WHERE {
  OPTIONAL { <ARTWORK_URI> write:hasSeal ?seal . }
  OPTIONAL { <ARTWORK_URI> write:hasColophon ?colophon . }
}
```

### CQ 1.8 — Which Chinese or other visual elements are present in the artwork?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?elementLabel
WHERE {
  <ARTWORK_URI> write:hasChineseVisualElement ?element .
  ?element rdfs:label ?elementLabel .
}
```
**Note:** Depending on the type of visual element, the following properties can be used:

- `write:hasChineseVisualElement` — Chinese visual elements
- `write:hasOtherVisualElement` — Other visual elements

### CQ 1.9 — Which Chinese concepts are represented in the artwork?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?conceptLabel
WHERE {
  <ARTWORK_URI> write:hasChineseConcept ?concept .
  ?concept rdfs:label ?conceptLabel .
}
```

### CQ 1.10 — Which topics are expressed in the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?topicLabel
WHERE {
  <ARTWORK_URI> wdt:P180 ?topic .
  ?topic rdfs:label ?topicLabel .
}
```
## Group 2 — Linguistic/Textual Analysis

### CQ 2.1 — In which language or languages is the content unit written?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?languageLabel
WHERE {
  <UNIT_URI> wdt:P407 ?language .
  ?language rdfs:label ?languageLabel .
}
```

### CQ 2.2 — Which writing system is used in the content unit?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?writingSystemLabel
WHERE {
  <UNIT_URI> wdt:P282 ?writingSystem .
  ?writingSystem rdfs:label ?writingSystemLabel .
}
```

### CQ 2.3 — When Chinese characters are used, which calligraphic script style is employed?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?scriptStyleLabel
WHERE {
  <UNIT_URI> wdt:P9302 ?scriptStyle .
  ?scriptStyle rdfs:label ?scriptStyleLabel .
}
```

### CQ 2.4 — Does the content unit contain a calligraphic line?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?hasCalligraphicLine
WHERE {
  <UNIT_URI> write:hasCalligraphicLine ?hasCalligraphicLine .
}
```

### CQ 2.5 — How many characters form the content unit?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?characterCount ?accuracy
WHERE {
  <UNIT_URI> write:numberOfCharacters ?characterCount .

  OPTIONAL {
    << <UNIT_URI> write:numberOfCharacters ?characterCount >>
       write:accuracy ?accuracy .
  }
}
```
**Note:** The character count may include an RDF-star annotation using `write:accuracy` to indicate the accuracy of the recorded value.

### CQ 2.6 — What is the writing direction of the content unit?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?direction
WHERE {
  <UNIT_URI> write:directionality ?direction .
}
```

### CQ 2.7 — Does the content unit carry semantic meaning, and how is that meaning classified?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?significance
WHERE {
  <UNIT_URI> write:hasSignificance ?significance .
}
```

### CQ 2.8 — Is the content unit based on a literary text?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?literaryWork
WHERE {
  <UNIT_URI> wdt:P144 ?literaryWork .
}
```

## Group 3 — Socio-Political-Economic Analysis

### CQ 3.1 — What is the educational background of the artist?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?fieldOfStudyLabel
WHERE {
  <PERSON_URI> wdt:P812 ?fieldOfStudy .
  ?fieldOfStudy rdfs:label ?fieldOfStudyLabel .
}
```

### CQ 3.2 — What is the calligraphic training of the artist?

```sparql
PREFIX write: <https://w3id.org/write/ontology#>

SELECT ?training
WHERE {
  <PERSON_URI> write:hasCalligraphicTraining ?training .
}
```

### CQ 3.3 — Where does the artist conduct their main artistic activity?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?placeLabel
WHERE {
  <PERSON_URI> wdt:P937 ?place .
  ?place rdfs:label ?placeLabel .
}
```

### CQ 3.4 — Where was the artwork created?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?placeLabel
WHERE {
  <ARTWORK_URI> wdt:P1071 ?place .
  ?place rdfs:label ?placeLabel .
}
```

### CQ 3.5 — Who commissioned the artwork, if anyone?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?commissioner
WHERE {
  <ARTWORK_URI> wdt:P88 ?commissioner .
}
```

### CQ 3.6 — What is the price of the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT ?price
WHERE {
  <ARTWORK_URI> wdt:P2284 ?price .
}
```

### CQ 3.7 — Who is the owner of the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?owner
WHERE {
  <ARTWORK_URI> wdt:P127 ?owner .
}
```

### CQ 3.8 — In which exhibitions has the artwork been presented?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>

SELECT DISTINCT ?exhibition
WHERE {
  <ARTWORK_URI> wdt:P608 ?exhibition .
}
```

### CQ 3.9 — What social, political, cultural, or economic topics are associated with the artwork?

```sparql
PREFIX wdt: <http://www.wikidata.org/prop/direct/>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>

SELECT DISTINCT ?topicLabel
WHERE {
  <ARTWORK_URI> wdt:P180 ?topic .
  ?topic rdfs:label ?topicLabel .
}
```
