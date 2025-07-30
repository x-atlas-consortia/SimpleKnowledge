# SimpleKnowledge 

This repository contains a set of spreadsheets in the 
SimpleKnowledge format, as described [here](doc/EditorUserGuide.md).

The UBKG generation framework ETL scripts obtain source information for a number of
SABs from the SimpleKnowledge spreadsheets in the _src_ directory.

# Types of SimpleKnowledge spreadsheets

The spreadsheets in this repository are of three types:
1. *Application ontologies* that provide configuration and operational information to support applications.
2. *Valuesets* of categorical information used to encode concepts
3. *Annotation mappings* used to link codes from a cell annotation protocol to codes in other ontologies.

# Contents
## Application ontologies
1. **SimpleKnowledgeHUBMAP**: application ontology for HuBMAP configuration in the UBKG
2. **SimpleKnowledgeSenNet**: application ontology for SenNet configuration in the UBKG
3. **SimpleKnowledgeUBKGSOURCE**: application ontology that describes the sources ingested into the UBKG.

## Annotation mappings
1. **SimpleKnowledgeAzimuth**: annotation mapping of Azimuth annotations to 
    + cell type codes in Cell Ontology
    + codes in UBERON
2. **SimpleKnowledgeDeepCellType**: annotation mapping of DeepCellType annotations to cell type codes in Cell Ontology
3. **SimpleKnowledgeSTELLAR**: annotation mapping of STELLAR annotations to
    + cell type codes in Cell Ontology
    + codes in UBERON
4. **SimpleKnowledgePanOrganAzimuth**: annotation of Pan Organ Azimuth annotations to
    + cell type codes in Cell Ontology
    + codes in UBERON

## Valuesets
1. **SimpleKnowledgeGenCode**: valueset to support the ingestion of GENCODE into the UBKG
2. **SimpleKnowledgeReactome**: valueset to support the ingestion of Reactome into the UBKG
3. **SimpleKnowledgeMTP_VS**: valueset to support the ingestion of data from the Molecular Targets Project (MTP) into the UBKG
4. **SimpleKnowledgeSenotype_VS**: valueset to support the ingestion of Senotype library data

