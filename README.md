---
output:
  pdf_document: default
  html_document: default
---

[![Open Source Love](https://badges.frapsoft.com/os/v3/open-source.png?v=103)](https://github.com/ellerbrock/open-source-badges/)


# Head-and-neck squamous cell carcinome co-expression networks of HPV+ samples

### Introduction

Head-and-neck squamous cell carcinoma (HNSCC) is a heterogeneous malignancy which accounts for approximately 300,000 deaths each year worldwide. Smoking, alcohol, and infections by high-risk human papillomavirus (HPV) are among the main risk factors for the development of the disease. The incidence of HPV-associated HNSCC is around 25% of the reported cases worldwide, with an even higher proportion in oropharyngeal cancer, and a predominance of infection by HPV-16 and HPV-18 types among those cases. 

The TCGA (The Cancer Genome Atlas) is paramount for data collection of more than 30 cancer types. The diversity of omic layers, such as RNA-seq, methylation, miRNA, proteomic, clinical, copy number variation and mutation, can be analyzed in different aspects including mathematical models, statistics and machine learning. 

### How to cite us

The article can be read on [`Scientific Reports`](http://dx.doi.org/10.1038/s41598-018-33498-5). DOI: 10.1038/s41598-018-33498-5.

### Network data model 

The graph data model (`Neo4j` database) was chosen to better explore the connectivity among genes in the co-expressed networks. This model consists mainly of nodes, edges and properties.  

![Figure 1: Data model representation with nodes and edges.](img/HPV-network.png).

### Neo4j

Neo4j is a highly scalable, robust (fully ACID) native graph database. Neo4j is used in mission-critical apps by thousands of startups, enterprises, and governments around the world.

### How to use

#### Install `Neo4j` (version 2.3.4) locally.

Visit the site: (https://neo4j.com/release-notes/neo4j-2-3-4/) and get the instructions on how to download, unzip, and install Neo4j.


#### Load the database

The database directory `hdscc.db` must be moved to `neo4j-community-xxx/data/`.

#### Change the configuration

You need to change the configuration. 

* Open the file: `/conf/neo4j-server.properties`.
* Change the line: `org.neo4j.server.database.location=data/graph.db` to `org.neo4j.server.database.location=data/hpv.db`.
* Save and close the file.

#### Start and use the database

* Start Neo4j: `./bin/neo4j start`. 
* Open the browser and access: http://localhost:7474.

### Simple queries

There are many possibilities of queries in a graph database using [Cypher](https://neo4j.com/developer/cypher-query-language/), a declarative SQL-inspired language. Here are two Cypher query examples:

Show all co-expressed genes and PPI interactions:

    MATCH (g:GENE)-[r:PPI_interaction]-(h:GENE)-[r2:Co_expression]-(g) 
    RETURN count(g)
    
Find the gene connections among two modues via PPI:

    MATCH (m:MODULE)-[r0:Belong]-(g:GENE)-[r:PPI_interaction]-(h:GENE)-[r2:Belong]-(mo:MODULE) 
    WHERE m.name="YellowHPV+" AND mo.name= "BlueHPV+" 
    RETURN DISTINCT g, m, h, mo
>
### Contact
If you have any comments or questions about this work which can improve it, please let us know! Thanks ;-)

**e-mail**: quelopes@gmail.com. 
<!-- Ask questions and please report any bug you find. -->
<!-- MATCH (m:MODULE)-[r0:Belong]-(g:GENE)-[r:PPI_interaction]-(h:GENE)-[r2:Co_expression]-(g) WHERE m.name="BlueHPV+" return g -->
<!-- MATCH (m:MODULE)-[r0:Belong]-(g:GENE)-[r:PPI_interaction]-(h:GENE)-[r2:Co_expression]-(g) WHERE m.name="YellowHPV+" return g -->
