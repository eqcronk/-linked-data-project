# Wine_data-linked-data-project
### OpenRefine, Schema.org, Wikidata, Turtle
## Overview
This project transforms wine data into RDF using Schema.org and Wikidata.
I used OpenRefine to clean data, reconcile to Wikidata and an RDF extension to turtle files.
# Dataset Description
This project transforms a wine dataset in RDF using OpenRefine. The data includes:
 - Wine name
 - Winery
 - Country
 - Province
 - Region 1
 - Region 2
 - Variety
 - Designation
 - Description
 - Price Taster name
Each row in the dataset represents a wine. The goal of this project is to transform this data into a graph where each wine is modeled as a schema:Product.
# Ontologies and Controlled Vocabularies Used
Schema.org
 schema:Product - wine
 schema:name - wine name
 schema:manufacturer - winery
 schema:countryOfOrigin - country
 schema:description - wine description provided by the manufacturer
 schema:category - designation/type
 schema:Offer - price information
 schema:Review - taster/review information
 schema:additionalProperty - Geographic information
Dublin Core
 dcterms:subject - wine variety
RDF
 rdf:type
Wikidata
 Locations
  wd:Q99   # California
  wd:Q824  # Oregon
 Wineries
 Tasters
 # Linking Strategy
This project used reconciliation in OpenRefine to link objects to Wikidata.
Columns such as province, region_1, region_2, country, winery, and taster_name are reconciled against Wikidata
The reconciled ID is extracted using: "cell.recon.match.id" in GREL
These IDs are exported as IRIs using wd
URI/IRI sets:
 country	Wikidata URI (wd:Q...)
 winery	Wikidata URI (wd:Q...)
 province	Wikidata URI via PropertyValue (wd:Q...)
 region_1	Wikidata URI via PropertyValue (wd:Q...)
 region_2	Wikidata URI via PropertyValue (wd:Q...)
 taster_name	Wikidata URI (wd:Q...)
Literal sets:
 "wine name"
 "description"
 "variety"
 "designation"
 "price"
# Sample Triples (starts at line 26 ends at line 53)
<https://example.org/Rainstorm_2013_Pinot_Gris_(Willamette_Valley)>
        schema:countryOfOrigin     wd:Q30 ;
        schema:additionalProperty  _:b4 ;
        schema:additionalProperty  _:b5 ;
        schema:review              _:b6 ;
        schema:offers              _:b7 ;
        dcterms:subject            "Pinot Gris" ;
        schema:name                "Rainstorm 2013 Pinot Gris (Willamette Valley)" ;
        schema:manufacturer        wd:Q133544744 ;
        rdf:type                   schema:Product ;
        schema:additionalProperty  _:b8 ;
        schema:description         "Tart and snappy, the flavors of lime flesh and rind dominate. Some green pineapple pokes through, with crisp acidity underscoring the flavors. The wine was all stainless-steel fermented." .

_:b9    schema:name   "region_2" ;
        schema:value  wd:Q11592 ;
        rdf:type      schema:PropertyValue .

_:b10   schema:priceCurrency  "USD" ;
        schema:price          "17"^^xsd:double ;
        rdf:type              schema:Offer .

_:b11   schema:priceCurrency  "USD" ;
        schema:price          "16"^^xsd:double ;
        rdf:type              schema:Offer .

_:b12   schema:name   "region_2" ;
        schema:value  wd:Q11592 ;
        rdf:type      schema:PropertyValue .
## Notes
 schema:name is constant value literal to differentiate between province, region_1 and region_2 ("province")
 schema:value contains the Wikidata identifier for province, region_1 and region_2 (wd:Q...)
 Blank nodes are used for Offer, Review, and PropertyValue
 Not all wines contain all fields
