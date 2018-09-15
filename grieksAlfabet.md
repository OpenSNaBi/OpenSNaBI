# Grieks alfabet

```sparql
SELECT DISTINCT ?entityOfInterest ?entityOfInterestLabel
  (GROUP_CONCAT(DISTINCT ?lowerCase; separator=", ") AS ?lowerCases)
  (GROUP_CONCAT(DISTINCT ?upperCase; separator=", ") AS ?upperCases)
WHERE {
  ?entityOfInterest wdt:P361 wd:Q8216 .

  { # lower case
    ?entityOfInterest ?pprop ?statement .
    wd:P487 wikibase:claim ?propp ;
            wikibase:statementProperty ?statementProp .
    ?statement ?qualifier wd:Q8185162 ;
               ?statementProp ?lowerCase .  
    wd:P518 wikibase:qualifier ?qualifier .
  }

  { # upper case
    ?entityOfInterest ?pprop2 ?statement2 .
    wd:P487 wikibase:claim ?propp2 ;
            wikibase:statementProperty ?statementProp2 .
    ?statement2 ?qualifier2 wd:Q98912 ;
               ?statementProp2 ?upperCase .  
    wd:P518 wikibase:qualifier ?qualifier2 .
  }
  SERVICE wikibase:label { bd:serviceParam wikibase:language "nl". }
} GROUP BY ?entityOfInterest ?entityOfInterestLabel

```
