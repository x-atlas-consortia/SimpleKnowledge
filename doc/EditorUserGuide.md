# SimpleKnowledge Knowledge Graph Editor User Guide

The SimpleKnowledge Editor is a tool to describe straightforward _ontologies_ that do not involve reasoning, based solely on assertion triplets. The SimpleKnowledge Editor is thus an alternative to OWL editors such as Stanford's [Protege](https://protege.stanford.edu/).

## Knowledge Graphs
The SimpleKnowledge Editor is a tool to build the source for a _RDF knowledge graph_. A knowledge graph can be considered to be a set of _assertions_. An assertion
defines a _relationship_ between two _entities_. 

In a graph database, an assertion is represented by two _nodes_ (representing the originating and terminating entities) linked by an _edge_ (representing the relationship). The combination of two nodes and a relationship is known as a _triplet_.

<img width="305" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/3bc06e6d-d0e1-41ec-b312-c517bb7cf020">

In graph databases such as neo4j, both nodes and edges can have attributes, or _properties_. A graph that contains assertions with nodes, edges, and properties is known as a _property graph_:

<img width="378" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/351ab72f-be2c-409c-9c88-d4189aa75a09">

A graph that represents properties as nodes is known as a _RDF graph_. For example, the properties *property 1* = A and *property 2* = B can be represented with nodes that are themselves in a hierarchy:

<img width="288" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/90014c2b-0c4d-40e1-bc0e-6451e48d4483">

## UBKG model
The SimpleKnowledge Editor is a Google Sheets solution to generate a RDF knowledge graph. The primary application of the SimpleKnowledge Editor is the creation of source that can be imported and translated into an instance of a [Unified Biological Knowledge Graph](https://ubkg.docs.xconsortia.org/).

The UBKG graph architecture is based on the UMLS model, in which a concept in a vocabulary (e.g., a SimpleKnowledge ontology) is represented with 
- a *Concept* node for the unique concept in the knowledge graph
- a *Code* node that the vocabulary uses to represent the concept
- a *Preferred Term*--a *Term* node of type _PT_
- one or more *Synonyms*-- *Term* nodes of type _SY_
- one or more *Definitions*-- *Definition* nodes
  
![image](https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/244a80e7-0a5c-4e72-bef4-74149b482b13)

### Concept cross-referencing
The UBKG also allows _concept cross-referencing_ (also known as *equivalence classes*), in which *Code* nodes share links to *Concept* nodes. When the code in a vocabulary is cross-referenced to a code in another vocabulary, the *Code* node is linked to the *Concept* node associated with the other *Code*. This allows for code synonymy by traversal across vocabularies. 

The following illustrates how "right kidney" is encoded in the UBKG in multiple vocabularies. The codes in the vocabularies share concept C0227613:

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

To build a SimpleKnowledge Editor for a knowledge graph, make a copy of the [Example SimpleKnowledge Editor](https://docs.google.com/spreadsheets/d/1D-rDOrqIuJ6DI-zoGlKMwPJ4ncw_au6_nSlJ_mlsw3U/edit?usp=sharing) document. Work in the sheet named *SimpleKnowledge Editor*.

The cells in the SimpleKnowledge Editor sheet represent the nodes and edges of the knowledge graph. The SimpleKnowledge Editor uses data validation rules to enforce the required structure of the nodes and edges.

## Node columns
To define a node, complete columns A-F.

### Column A (term)
This is the required *preferred term* for the node. 
The term must be unique.

### Column B (code)
This is the code for the node in the ontology represented by the SimpleKnowledge Editor.
The format of the code should be _SAB_:_CODE_, in which _SAB_ is an acronym for ontology.
Codes must be unique.

### Column C (definition)
This is an optional definition for the code.

### Column D (synonyms)
This is an optional list of synonyms for the code. The list should be pipe-delimited.

### Column E (dbxref)
Identifier for the optional equivalence class(es) or cross-reference(s) for the code. 
Identifiers can be in format:
- Concept Unique Identifier
- Code in another vocabulary

If a code can be cross-referenced to multiple entities, the entities should be in a pipe-delimited list--i.e.,
`<SAB1:CODE1>|<SAB2:CODE2>`

### Example node row
| term | code | definition | synonym| dbxref   |
| --- | --- | --- | --- | ---|
| Color | ABC:C001 | visual perception based on the electromagnetic spectrum| hue\|cast\|tint | UMLS:C0009393|

## Edge columns

### Column F (isa)
Column F defines _isa_, or hierchical, edges between code nodes.
A code can be in multiple _isa_ hierarchies. To define multiple hierarchies, use comma delimiting in the *isa* column.
Identify a node for an _isa_ relationship using the term in column A, not the code in colum B.

#### Example

The **ABC:C003** (blue) code is a member of two hierarchies--one with parent **ABC:C001** (Color) and one with parent **ABC:C002** (Emotion).

| term | code | definition | synonym| dbxref   | isa|
| --- | --- | --- | --- | ---| ---|
| Color | ABC:C001 | visual perception based on the electromagnetic spectrum| hue\|cast\|tint | UMLS:C0009393| |
| Emotion | ABC:C002 | physical and mental states brought on by neurophysiological changes| feeling | | |
| blue| ABC:C003 | | | |Color,Emotion|

#### Rules for isa hierarchies
1. There must be a _root_ node with no value in the *isa* column.
2. All other nodes must have at least one reference in the *isa* column.
3. Values in *isa* must be terms in Column A.

### Custom edges
The columns after F can be used to define custom edges.
The cell that intersects a node row and an edge column defines the edge between the node's row and other nodes.

#### Example

Note:
1. The **thing** root node.
2. The **Color**, **Emotion**, and **sky** nodes are all members of the **thing** hierarchy.
3. The **blue** node is a member of both the **Color** and **Emotion** hierarchies.
4. The **cyan** and **azure** nodes are children of **blue**, and thus are in the **Color** hierarchy.
5. The **sky** node is used in the **used_to_describe** custom edge column. This represents the assertion **azure** _used_to_describe_ **sky**.

| term | code | definition | synonym| dbxref   | isa| used_to_describe |
| --- | --- | --- | --- | ---| ---| --- |
| thing| ABC:C000 | root |||| |
| Color | ABC:C001 | visual perception based on the electromagnetic spectrum| hue\|cast\|tint | UMLS:C0009393|thing | |
| Emotion | ABC:C002 | physical and mental states brought on by neurophysiological changess| feeling | |thing | |
| blue| ABC:C003 | | | |Color,Emotion| |
|cyan| ABC:C004| | | | blue| |
|azure| ABC:C005||| |blue| sky|
|sky| ABC:C006||||thing| |

This will result in a graph similar to

<img width="341" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/c4ccc7b0-ac93-42e6-9785-eb7c713342c0">

# Visualization
It is possible to visualize parts of a SimpleKnowledge knowledge graph using the custom **guesdt** application. **guesdt** is a Javascript app that works with the SimpleKnowledge source in Google Sheet.

To visualize a SimpleKnowledge graph, enter into a browser a URL in format https://guesdt.com/SimpleKnowledgeVisualization.html?sheet=sheetid.

Obtain the id for the Google Sheet used by the **guesdt** from the URL that points to the Google Sheet--e.g.,

https://docs.google.com/spreadsheets/d/1D-rDOrqIuJ6DI-zoGlKMwPJ4ncw_au6_nSlJ_mlsw3U/edit#gid=952245609

The following image is from the visualization of the example SimpleKnowledge graph. Note that the visualization automatically creates inverse relationships (e.g., _inverse_isa_).

<img width="1217" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/a02f0666-ce7a-480f-809d-5bb36026bdb8">




