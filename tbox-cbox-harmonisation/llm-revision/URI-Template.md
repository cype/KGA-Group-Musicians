**Namespaces**

| Prefix       | Namespace                                                        | Contains                                                                 |
| ------------ | ---------------------------------------------------------------- | ------------------------------------------------------------------------ |
| `musicians:` | `https://www.knowledge-graph-guys.com/music-ontology/musicians#` | Schema: ontology classes, properties, and controlled vocabulary concepts |
| `data:`      | `https://www.knowledge-graph-guys.com/music-ontology/data#`      | Data: concrete people, bands, careers, memberships, and movie records    |
| `inst:`      | `http://instruments.knowledge-graph-guys.com/`                   | Instrument instances used by musicians                                   |
| `schema1:`   | `http://schema.org/`                                             | External schema.org properties and classes                               |
| `skos:`      | `http://www.w3.org/2004/02/skos/core#`                           | Controlled vocabulary structure for roles and languages                  |
| `wd:`        | `http://www.wikidata.org/entity/`                                | Wikidata mappings                                                        |
| `imdb:`      | `https://www.imdb.com/title/`                                    | IMDb movie identifiers                                                   |

The `musicians:` namespace defines what kinds of things exist: classes, properties, roles, languages, and controlled values.

The `data:` namespace contains the actual instances, such as musicians, bands, careers, band memberships, and movies.

**URI Templates**

Here are the URI templates from the current musicians ontology:

| Class / Concept Type       | Description                                        | URI Template                                                                                                                                | Example                                                                                                                       |
| -------------------------- | -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| `musicians:Person`         | A musician or music-related person                 | `https://www.knowledge-graph-guys.com/music-ontology/data#{{ personName \| slug }}`                                                         | `https://www.knowledge-graph-guys.com/music-ontology/data#paul-mccartney`                                                     |
| `musicians:Band`           | A musical group or band                            | `https://www.knowledge-graph-guys.com/music-ontology/data#{{ bandName \| slug }}`                                                           | `https://www.knowledge-graph-guys.com/music-ontology/data#the-beatles`                                                        |
| `musicians:BandMembership` | A time-bounded membership of a person in a band    | `https://www.knowledge-graph-guys.com/music-ontology/data#band-membership-{{ personName \| slug }}-{{ bandName \| slug }}-{{ startDate }}`  | `https://www.knowledge-graph-guys.com/music-ontology/data#band-membership-paul-mccartney-the-beatles-1960-01-01`              |
| `musicians:MusicalCareer`  | A musical career or career phase of a person       | `https://www.knowledge-graph-guys.com/music-ontology/data#{{ personName \| slug }}-career{% if context %}-{{ context \| slug }}{% endif %}` | `https://www.knowledge-graph-guys.com/music-ontology/data#paul-mccartney-career-beatles`                                      |
| `musicians:Movie`          | A movie connected to a musician                    | `https://www.knowledge-graph-guys.com/music-ontology/data#{{ personName \| slug }}-role-in-{{ movieTitle \| slug }}`                        | `https://www.knowledge-graph-guys.com/music-ontology/data#taylor-swift-role-in-the-movie-a-beautiful-day-in-the-neighborhood` |
| `musicians:MusicalRole`    | A controlled vocabulary concept for a musical role | `https://www.knowledge-graph-guys.com/music-ontology/musicians#{{ roleName \| pascalCase }}`                                                | `https://www.knowledge-graph-guys.com/music-ontology/musicians#PopSinger`                                                     |
| `musicians:Language`       | A controlled vocabulary concept for a language     | `https://www.knowledge-graph-guys.com/music-ontology/musicians#{{ languageName \| pascalCase }}`                                            | `https://www.knowledge-graph-guys.com/music-ontology/musicians#English`                                                       |
| `musicians:DegreeOfFame`   | A controlled value for how famous a musician is    | `https://www.knowledge-graph-guys.com/music-ontology/musicians#{{ fameLevel \| pascalCase }}Fame`                                           | `https://www.knowledge-graph-guys.com/music-ontology/musicians#NationalFame`                                                  |
| `inst:Instrument`          | A musical instrument played by a person            | `http://instruments.knowledge-graph-guys.com/{{ instrumentName \| slug }}`                                                                  | `http://instruments.knowledge-graph-guys.com/bass-guitar`                                                                     |
| `skos:ConceptScheme`       | A scheme grouping controlled vocabulary concepts   | `https://www.knowledge-graph-guys.com/music-ontology/musicians#{{ schemeName \| pascalCase }}`                                              | `https://www.knowledge-graph-guys.com/music-ontology/musicians#MusicalRoles`                                                  |

**Main Classes**

| Class                      | Meaning                                                         |
| -------------------------- | --------------------------------------------------------------- |
| `musicians:Person`         | A person involved in music                                      |
| `musicians:Band`           | A musical group                                                 |
| `musicians:BandMembership` | A link between a person and a band, with start and end dates    |
| `musicians:MusicalCareer`  | A musical career or career phase                                |
| `musicians:MusicalRole`    | A role such as singer, songwriter, instrumentalist, or producer |
| `musicians:Language`       | A language spoken by a person                                   |
| `musicians:DegreeOfFame`   | A fame level such as local, national, or international fame     |
| `musicians:Movie`          | A movie connected to a musician                                 |

**Main Relationship Patterns**

| Property                         | Domain                     | Range                      | Meaning                                                            |
| -------------------------------- | -------------------------- | -------------------------- | ------------------------------------------------------------------ |
| `musicians:hasCareer`            | `musicians:Person`         | `musicians:MusicalCareer`  | Connects a person to a musical career                              |
| `musicians:hasRole`              | `musicians:MusicalCareer`  | `musicians:MusicalRole`    | Assigns musical roles to a career                                  |
| `musicians:plays`                | `musicians:Person`         | `inst:Instrument`          | States that a person plays an instrument                           |
| `musicians:hasPrimaryInstrument` | `musicians:Person`         | `inst:Instrument`          | States a person’s main instrument                                  |
| `musicians:memberOf`             | `musicians:Person`         | `musicians:Band`           | Connects a person directly to a band                               |
| `musicians:hasBandMembership`    | `musicians:Person`         | `musicians:BandMembership` | Connects a person to a detailed band membership record             |
| `musicians:membershipBand`       | `musicians:BandMembership` | `musicians:Band`           | States which band a membership belongs to                          |
| `musicians:membershipStartDate`  | `musicians:BandMembership` | `xsd:date`                 | Start date of a band membership                                    |
| `musicians:membershipEndDate`    | `musicians:BandMembership` | `xsd:date`                 | End date of a band membership                                      |
| `musicians:hasDegreeOfFame`      | `musicians:Person`         | `musicians:DegreeOfFame`   | States whether a person has local, national, or international fame |
| `musicians:speaks`               | `musicians:Person`         | `musicians:Language`       | Connects a person to a spoken language                             |
| `musicians:hasRoleInMovie`       | `musicians:Person`         | `musicians:Movie`          | Connects a person to a movie they are associated with              |
