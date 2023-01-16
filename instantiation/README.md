# Blockchain-based Ontology Driven Reference Framework (OntRef) Instantiation

We [instantiated](https://github.com/mubashar-iqbal/OntRef/blob/main/instantiation/OntRef-instantiation.owl) the [OntRef](https://github.com/mubashar-iqbal/OntRef) with the data tampering threat and Sybil attack.

## SPARQL queries
The SPARQL queries can be used to retrieve information from an OntRef instantiation ontology. The following header code will remain the same for all the queries listed in this section.

```sql
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX owl: <http://www.w3.org/2002/07/owl#>
PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

PREFIX OntRef_INST: <https://mmisw.org/ont/~mubashar/OntRef-instantiation#>
```

### System assets
The following SPARQL query retrieves the system assets that support the business assets.

```sql
SELECT DISTINCT ?System_asset ?Business_asset WHERE {
    ?System_asset rdfs:subClassOf OntRef_INST:SystemAsset .
    ?System_asset rdfs:subClassOf ?Business_asset .
    ?Business_asset owl:onProperty OntRef_INST:supports .
}
```

### Business assets
The following SPARQL query gets the business assets that have the security criteria constraint.

```sql
SELECT DISTINCT ?Business_asset ?Constraint WHERE {
    ?Business_asset rdfs:subClassOf OntRef_INST:BusinessAsset .
    ?Business_asset rdfs:subClassOf ?Constraint .
    ?Constraint owl:onProperty OntRef_INST:hasConstraint .
    { ?Constraint owl:someValuesFrom OntRef_INST:Confidentiality . }
    UNION
    { ?Constraint owl:someValuesFrom OntRef_INST:Integrity . }
    UNION
    { ?Constraint owl:someValuesFrom OntRef_INST:Availability . }
}
```

### Threats mitigated
The following SPARQL query brings the threats that are mitigated by using the blockchain for a smart healthcare system. The query result shows the threats mitigated, associated vulnerabilities, and system assets that are targeted by the threats.

```sql
SELECT DISTINCT ?Threat ?Vulnerability ?System_asset WHERE {
    ?Threat rdfs:subClassOf ?Vulnerability .
    ?Threat rdfs:subClassOf ?System_asset .
    ?Vulnerability owl:onProperty OntRef_INST:exploits .
    ?System_asset owl:onProperty OntRef_INST:targets .
    ?Threat rdfs:seeAlso ?Domain .
    FILTER regex(?Domain, "^Mitigated")
}
```
### Threats appeared
The following SPARQL query brings the threats that are appeared within a blockchain-based smart healthcare system. The query result shows the threats appeared, associated vulnerabilities, and system assets that are targeted by the threats.

```sql
SELECT DISTINCT ?Threat ?Vulnerability ?System_asset WHERE {
    ?Threat rdfs:subClassOf ?Vulnerability .
    ?Threat rdfs:subClassOf ?System_asset .
    ?Vulnerability owl:onProperty OntRef_INST:exploits .
    ?System_asset owl:onProperty OntRef_INST:targets .
    ?Threat rdfs:seeAlso ?Domain .
    FILTER regex(?Domain, "^Appeared")
}
```

### Countermeasure
The following SPARQL query brings the list of countermeasures to mitigate the threats.

```sql
SELECT DISTINCT ?Countermeasure ?Vulnerability WHERE {
    ?Countermeasure rdfs:subClassOf OntRef_INST:Countermeasure .
    ?Countermeasure rdfs:subClassOf ?Vulnerability .
    ?Vulnerability owl:onProperty OntRef_INST:mitigates .
}
```

## Classification of OntRef instantiation
Protégé-based classification illustrates the class hierarchies along with their defined relationships.

<img src="OntRef-instantiation.png" width="450" alt="OntRef Protégé-based classifications" title="OntRef Protégé-based classifications"/>

### Class hierarchies

OntRef instantiation "is-a" based taxonomical structure illustrates the class hierarchies.

<img src="OntRef_classes_hierarchy.png" width="450" alt="OntRef Protégé-based classifications" title="OntRef Protégé-based classifications"/>

## How to use?
Download [Protégé](https://protege.stanford.edu) editor. Load/import [OntRef instantiation](https://mmisw.org/ont/~mubashar/OntRef-instantiation) in Protégé and navigate to the *Entities* tab. You can also execute the above-listed SPARQL queries to explore the encoded security risk management concepts.