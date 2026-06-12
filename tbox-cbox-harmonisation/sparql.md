```
# Which internationally famous instrumentalists play the guitar?

PREFIX musicians: <https://www.knowledge-graph-guys.com/music-ontology/musicians#>
PREFIX schema: <http://schema.org/>
PREFIX inst: <http://instruments.knowledge-graph-guys.com/>

SELECT ?fullName ?role ?degreeOfFame
WHERE {
    ?person schema:givenName ?givenName ;
            schema:familyName ?familyName ;
            musicians:plays inst:bass-guitar ;
            musicians:hasCareer ?career ;
            musicians:hasDegreeOfFame ?degreeOfFame .

    FILTER(?degreeOfFame = musicians:InternationalFame)

    ?career musicians:hasRole ?role .

    BIND(CONCAT(?givenName, " ", ?familyName) AS ?fullName)
}
```

https://atomgraph.github.io/SPARQL-Playground/<br>

https://docs.google.com/document/d/1Cb0I78dBxjR_1xUavPHxwNQld4UI8OhLkvDEL-a18MM/edit?tab=t.0