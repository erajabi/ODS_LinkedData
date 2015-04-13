# Welcome to the ODS_LinkedData wiki! 

Open Discovery Space aggregated a large number of eLearning metadata, which were in IEEE LOM standard. We exposed all the ODS metadata as Linked Data in the following step:

## Converting the XML files into RDF
We wrote a JAVA program to read the final ODS metadata files one by one and convert it to RDF using an instruction which is available at [here](http://data.opendiscoveryspace.eu/ODS_LOM2LD/ODS_SecondDraft.html). According to the mentioned instruction, we created an ontology, at [here](http://data.opendiscoveryspace.eu/lom_ontology_ods.owl#), and exposed the most important elements as RDF using Java libraries (Jena). 

## Dividing the final RDF dump into chunks
The final created RDF dump was around 1 GB. That's why, we used tdbloader command to divide it to chunks. 
we used [apache-jena-2.13.0](http://jena.apache.org/download/index.cgi), which includes a "bat" folder and TDB commands are available at there. We also used jena-fuseki-1.0.1-distribution as our triple store manager.

`tdbloader --loc=ODSTripleStore ODSFullDump.ttl`

* ODSTripleStore is an existing TDB database folder. Create an empty one if it does not exist.
* The second parameter is the RDF dump.

## Importing the RDF chunks into a triple store
Fuseki is a SPARQL server. It provides REST-style SPARQL HTTP Update, SPARQL Query, and SPARQL Update using the SPARQL protocol over HTTP. <br>
Then we ran [Jena Fuseki ](http://jena.apache.org/documentation/serving_data/) by the following command at top of the our triple store:

`fuseki-server --loc=ODSTripleStore /ods` 

For more information about configuring Jena Fuseki you can read [here ](http://jena.apache.org/documentation/serving_data/)
