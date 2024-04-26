# SimpleKnowledge Knowledge Graph Editor User Guide

## Knowledge Graphs
The SimpleKnowledge Editor is a tool to build the source for a _RDF knowledge graph_. A knowledge graph can be considered to be a set of _assertions_. An assertion
defines a _relationship_ between two _entities_. 

In a graph database, an assertion is represented by two _nodes_ (representing the originating and terminating entities) linked by an _edge_ (representing the relationship). The combination of two nodes and a relationship is known as a _triplet_.

<img width="305" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/3bc06e6d-d0e1-41ec-b312-c517bb7cf020">

In graph databases such as neo4j, both nodes and edges can have attributes, or _properties_. A graph that contains assertions with nodes, edges, and properties is known as a _property graph_:

<img width="378" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/351ab72f-be2c-409c-9c88-d4189aa75a09">

A graph that represents properties as nodes is known as a _RDF graph_. For example, the properties *property 1* = A and *property 2* = B can be represented with nodes that are themselves in a hierarchy:

<img width="288" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/90014c2b-0c4d-40e1-bc0e-6451e48d4483">

## SimpleKnowledge Editor
The SimpleKnowledge Editor is a Google Sheets solution to generate a RDF knowledge graph. The primary application of the SimpleKnowledge Editor is the creation of source that can be imported and translated into an instance of a [Unified Biological Knowledge Graph](https://ubkg.docs.xconsortia.org/).

The UBKG graph architecture is based on the UMLS model, in which a concept in a vocabulary (e.g., a SimpleKnowledge ontology) is represented with 
- a *Concept* node for the unique concept in the knowledge graph
- a *Code* node that the vocabulary uses to represent the concept
- a *Preferred Term*--a *Term* node of type _PT_
- one or more *Synonyms*-- *Term* nodes of type _SY_
- one or more *Definitions*-- *Definition* nodes
  
![image](https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/244a80e7-0a5c-4e72-bef4-74149b482b13)

### Concept cross-referencing
The UBKG also allows _concept cross-referencing_, in which *Code* nodes share links to *Concept* nodes. When the code in a vocabulary is cross-referenced to a code in another vocabulary, the *Code* node is linked to the *Concept* node associated with the other *Code*. This allows for concept synonymy by traversal across vocabularies. 

For example, the following illustrates how "right kidney" is encoded in the UBKG in multiple vocabularies. The codes in the vocabularies share concept C0227613:

<img width="450" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/2e23ffef-9042-4649-8509-a0ed8c5b7add">

| Code  | Term |
| ------------- | ------------- |
| SENNET:C030030  | Kidney (Right)  |
| HUBMAP:C030059  | Kidney (Right) |
| NCI:C34005 | Right Kidney|
|UWDA:7204| Right kidney|
| SNOMEDCT_US:9846003|Right kidney structure|
| UBERON:0004539| right kidney|
|CHV:0000022146|right kidney|

# Building a SimpleKnowledge Editor

It is possible with the SimpleKnowledge Editor to describe straightforward _ontologies_ that do not involve reasoning--i.e., based solely on assertion triplets. The SimpleKnowledge Editor is thus an alternative to OWL editors such as Stanford's [Protege](https://protege.stanford.edu/).

To build a SimpleKnowledge Editor for a knowledge graph, make a copy of the [Example SimpleKnowledge Editor](https://docs.google.com/spreadsheets/d/1D-rDOrqIuJ6DI-zoGlKMwPJ4ncw_au6_nSlJ_mlsw3U/edit?usp=sharing) document. Work in the sheet named *SimpleKnowledge Editor*.

The cells in the SimpleKnowledge Editor sheet represent the nodes and edges of the knowledge graph. The SimpleKnowledge Editor uses data validation rules to enforce the required structure of the nodes and edges.

