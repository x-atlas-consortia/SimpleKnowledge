# SimpleKnowledge Knowledge Graph Editor User Guide

## Knowledge Graphs
The SimpleKnowledge Editor is a tool to build the source for a _RDF knowledge graph_. A knowledge graph can be considered to be a set of _assertions_. An assertion
defines a _relationship_ between two _entities_. 

In a graph database, an assertion is represented by two _nodes_ (representing the originating and terminating entities) linked by an _edge_ (representing the relationship):

<img width="305" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/3bc06e6d-d0e1-41ec-b312-c517bb7cf020">

In graph databases such as neo4j, both nodes and edges can have attributes, or _properties_. A graph that contains assertions with nodes, edges, and properties is known as a _property graph_:

<img width="378" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/351ab72f-be2c-409c-9c88-d4189aa75a09">

A graph that represents properties as nodes is known as a _RDF graph_. For example, the properties *property 1* = A and *property 2* = B can be represented with nodes that are themselves in a hierarchy:

<img width="288" alt="image" src="https://github.com/x-atlas-consortia/SimpleKnowledge/assets/10928372/90014c2b-0c4d-40e1-bc0e-6451e48d4483">

## SimpleKnowledge Editor
The SimpleKnowledge Editor is a Google Sheets solution to generate a RDF knowledge graph. The primary application of the SimpleKnowledge Editor is the creation of source that is imported and translated into an instance of a [Unified Biological Knowledge Graph](https://ubkg.docs.xconsortia.org/)

It is possible with the SimpleKnowledge Editor to describe ontologies that do not involve reasoning--i.e., ontologies based solely on assertions. The SimpleKnowledge Editor is thus an alternative to OWL editors such as Stanford's [Protege](https://protege.stanford.edu/).
