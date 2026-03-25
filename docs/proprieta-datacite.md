# Proprietà di DataCite

La descrizione del DataCite Metadata Schema 4.6 si trova [qui](https://datacite-metadata-schema.readthedocs.io/en/4.6/).

## Interfaccia ```oai_datacite```

Per l'uscita nello schema [OAI Datacite](https://schema.datacite.org/oai/oai-1.1/) (```metadataPrefix=oai_datacite```), utilizzare i seguenti elementi

```xml
<oai_datacite xsi:schemaLocation="http://schema.datacite.org/oai/oai-1.1/ http://schema.datacite.org/oai/oai-1.1/oai.xsd" >
    <schemaVersion>4.6</schemaVersion>
    <datacentreSymbol>UNIBO.ASDD</datacentreSymbol>
    <payload>
        <resource xsi:schemaLocation="http://datacite.org/schema/kernel-4 http://schema.datacite.org/meta/kernel-4.6/metadata.xsd" >
            ...
        </resource>
    </payload>
</oai_datacite>
```

## 1. Identifier

Utilizziamo il campo ```doi```.

=== "AMS Acta json" 

    ```json
    {
        "doi": "10.13123/unibo/amsactatest/7009"
    }
    ```

=== "DataCite xml"

    ```xml
    <identifier identifierType="DOI">10.13123/unibo/amsactatest/7009</identifier>
    ```

## 2. Creator

I creators e le sottoproprietà sono presi dal campo ```creators```. Nel caso in cui esistano sia il campo ```given``` sia il campo ```family```, allora la proprietà ```creatorName``` deve avere l'attributo ```nameType="Personal"```

=== "AMS Acta json"

    ```json
    "creators": [
        {
        "id": "vito.baldassarro@unibo.it",
        "affiliation": "University of Bologna",
        "orcid": "0000-0003-1020-4261",
        "name": {
            "honourific": null,
            "lineage": null,
            "family": "Baldassarro",
            "given": "Vito Antonio"
        }
        },
        {
        "orcid": "0009-0004-0124-1110",
        "ror": "https://ror.org/01111rn36",
        "name": {
            "honourific": null,
            "lineage": null,
            "given": "Quentin",
            "family": "Brassart"
        },
        "affiliation": "Institute de Génétique et de Biologie Moléculaire et Cellulaire, Université de Strasbourg",
        "id": "brassarq@igbmc.fr"
        }
    ]
    ```

=== "DataCite xml"

    ```xml
    <creators>
        <creator>
            <creatorName nameType="Personal">Baldassarro, Vito Antonio</creatorName>
            <givenName>Vito Antonio</givenName>
            <familyName>Baldassarro</familyName>
            <affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">University of Bologna</affiliation>
            <nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0000-0002-9494-5384</nameIdentifier>
        </creator>
        <creator>
            <creatorName>Brassart, Quentin</creatorName>
            <givenName>Quentin</givenName>
            <familyName>Brassart</familyName>
            <affiliation affiliationIdentifier="https://ror.org/00pg6eq24" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">, Université de Strasbourg</affiliation>
            <nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0009-0004-0124-1110</nameIdentifier>
        </creator>
    </creators>
    ```

Nel caso in cui sia presente solo il cognome, allora ```nameType``` è ```"Organizational"```.

=== "AMS Acta json"
    
    ```json
    "creators": {
        "name": {
            "lineage": null,
            "given": null,
            "honourific": null,
            "family": "Università degli Studi di Bologna"
        },
        "ror": "https://ror.org/01111rn36"
    }
    ```

=== "DataCite XML"

    ```xml
    <creators>
        <creator>
            <creatorName nameType="Organizational">Università degli Studi di Bologna</creatorName>
            <nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ROR">https://ror.org/01111rn36</nameIdentifier>
        </creator>
    </creators>
    ```

Il campo Creator è obbligatorio. Come fare quando non ci sono creators ma solo contributors (come nel caso di curatele).

## 3. Title

Si utilizza il campo ```title```. La lingua viene presa dalla lingua del primo file allegato 

=== "AMS Acta json" 

    ```json
    { 
        "title": "Data about the role of RXRγ in T3-mediated oligodendrocyte precursor cell differentiation",
        "documents": [
            {
            "language": "en",
            "pos": 1,
            }
        ]
    }
    ```

=== "DataCite xml"

    ```xml
    <titles>
        <title xml:lang="en">Data about the role of RXRγ in T3-mediated oligodendrocyte precursor cell differentiation</title>
    </titles>
    ```

Al momento il titolo non è duplicabile. Non esponiamo l'attributo ```titleType```.

## 4. Publisher

Valutare in futuro se aggiungere il ROR dell'editore.

=== "AMS Acta json" 
    ```json
    {
        "publisher": "University of Bologna"
    }
    ```
=== "DataCite xml"
    ```xml
    <publisher>University of Bologna</publisher>
    ```

## 5. PublicationYear

Nel file ```z_datacite_mapping.pl``` si specifica che

```perl
# publicationYear this is derived from the eprint.date (this will have the pub date if datesdatesdates is in play)
# https://schema.datacite.org/meta/kernel-4.0/metadata.xsd#publicationYear
# Year when the data is made publicly available. 
# If an embargo period has been in effect, use the date when the embargo period ends.
```

Bisogna invece prendere l'anno dalla data inserita nel campo data. Alternativamente:

- Pubblicato
- Invio all’editore
- Fine della stesura

È importante non utilizzare la data di deposito (```datestamp```) perché alcuni autori hanno la necessità di retrodatare la data di pubblicazione.

=== "AMS Acta json" 
    ```json
    {
        "date": "2022-11-15",
        "date_type": "submitted",
    }
    ```

=== "DataCite xml"
    ```xml
    <publicationYear>2022</publicationYear>
    ```

Per le altre date vedere il la sezione [Date](#8-date).

## 6. Subject

OK mappare le keywords, separandole con la virgola o i punto e virgola.

Occorre anche inserire gli SSD e gli ERC panels.

Problema con la lingua. Per le keywords, usare la lingua del primo documento caricato. Per gli SSD occorre usare ```xml:lang="it"```. Per gli ERC panels usare ```xml:lang="en"```.

In futuro devono essere aggiornate gli SSD e gli ERC panels con i nuovi codici vigenti dal 2024.

Soluzione di minima, senza gli attributi subjectScheme, schemeURI e valueURI.

=== "AMS Acta json" 

    ```json
    {
        "keywords": "urban spaces, metropolis, cities, digital technologies, automation, AI, smart city",
        "documents": [
            {
                "language": "en",
                "pos": 1,
            },
        ],
        "subjects": [
            "M-GGR-01",
            "SPS-10",
            "SH2_11",
        ],
    }
    ```

=== "DataCite xml"

    ```xml
    <subjects>
        <subject xml:lang="en">urban spaces</subject>
        <subject xml:lang="en">metropolis</subject>
        <subject xml:lang="en">cities</subject>
        <subject xml:lang="en">digital technologies</subject>
        <subject xml:lang="en">automation</subject>
        <subject xml:lang="en">AI</subject>
        <subject xml:lang="en">smart city</subject>
        <subject xml:lang="it">M-GGR-01 Geografia</subject>
        <subject xml:lang="it">SPS-10 Sociologia dell'ambiente e del territorio</subject>
        <subject xml:lang="en">SH2-11 Human, economic and social geography</subject>
    </subjects>
    ```

Soluzione ottimale, aggiungendo gli attributi subjectScheme, schemeURI e valueURI degli ERC e degli SSD.

=== "DataCite xml"

    ```xml
    <subjects>
        <subject xml:lang="en">urban spaces</subject>
        <subject xml:lang="en">metropolis</subject>
        <subject xml:lang="en">cities</subject>
        <subject xml:lang="en">digital technologies</subject>
        <subject xml:lang="en">automation</subject>
        <subject xml:lang="en">AI</subject>
        <subject xml:lang="en">smart city</subject>
        <subject xml:lang="it" subjectScheme="Classificazione degli ambiti disciplinari" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines/019-011">M-GGR-01 Geografia</subject>
        <subject xml:lang="it" subjectScheme="Classificazione degli ambiti disciplinari" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines/025-010">SPS-10 Sociologia dell'ambiente e del territorio</subject>
        <subject xml:lang="en" subjectScheme="Vocabolario Controllato 2019 ERC EVALUATION PANEL e KEYWORD" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-her/erc-panel-h2020-fp" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-her/erc-panel-h2020-fp/SH2-11">SH2-11 Human, economic and social geography</subject>
    </subjects>
    ```

## 7. Contributor

Il metadato da mappare è ```contributors```.

=== "AMS Acta json"

    ```json
    "contributors": [
        {
        "affiliation": "Università di Bologna",
        "name": {
            "lineage": null,
            "family": "Katarina",
            "given": "Lučić",
            "honourific": null
        },
        "orcid": "0009-0008-0919-301X",
        "type": "DataManager"
        },
        {
        "affiliation": "Università di Bologna",
        "orcid": "0000-0001-8803-8940",
        "name": {
            "honourific": null,
            "lineage": null,
            "family": "Iezzi",
            "given": "Adriana"
        },
        "type": "ContactPerson"
        }
    ]
    ```

=== "DataCite xml"

    ```xml
    <contributors>
        <contributor contributorType="DataManager">
            <contributorName nameType="Personal">Katarina, Lučić</contributorName>
            <givenName>Lučić</givenName>
            <familyName>Katarina</familyName>
            <nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0009-0008-0919-301X</nameIdentifier>
            <affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">Università di Bologna</affiliation>
        </contributor>
        <contributor contributorType="ContactPerson">
            <contributorName nameType="Personal">Iezzi, Adriana</contributorName>
            <givenName>Adriana</givenName>
            <familyName>Iezzi</familyName>
            <nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0000-0001-8803-8940</nameIdentifier>
            <affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">Università di Bologna</affiliation>
        </contributor>
    </contributors>
    ```

Bisogna aggiornare la lista dei tipi di contributor (contributorType). Ecco la lista

```
ContactPerson
DataCollector
DataCurator
DataManager
Distributor
Editor
HostingInstitution
Producer
ProjectLeader
ProjectManager
ProjectMember
RegistrationAgency
RegistrationAuthority
RelatedPerson
Researcher
ResearchGroup
RightsHolder
Sponsor
Supervisor
Translator
WorkPackageLeader
Other
```

Mantenere nella lista

```
Funder
```

Nella nuova lista occorre inserire solo ```Translator```.

### Capitoli di libro senza ```creators```

=== "AMS Acta json"

    ```json
    {
        "eprintid": 6055,
        "curators": [ // curatori della serie, non lo mappiamo su DataCite
        {
            "name": {
                "honourific": null,
                "lineage": null,
                "given": "Stefano",
                "family": "Ferrari"
            },
            "affiliation": "Università di Bologna",
            "id": "stefano.ferrari@unibo.it"
        }
        ],
        "book_curators": [ // curatori del libro, da mappare su relatedItem
        {
            "id": "laura.ricca2@unibo.it",
            "affiliation": "Università di Bologna",
            "name": {
                "family": "Ricca",
                "given": "Laura",
                "lineage": null,
                "honourific": null
            }
        }
        ],
        "editors": [ // curatori del capitolo di libro, da mappare su creators se non esistono creators
        {
            "name": {
                "honourific": null,
                "lineage": null,
                "family": "Milani",
                "given": "Raffaele"
            },
            "affiliation": "Università di Bologna"
        }
        ],
    }
    ```

=== "DataCite xml"

    ```xml
    <creators>
        <creator>
            <creatorName nameType="Personal">Milani, Raffaele</creatorName>
            <givenName>Raffaele</givenName>
            <familyName>Milani</familyName>
            <affiliation>Università di Bologna</affiliation>
        </creator>
    </creators>
    ```

### Capitoli di libro con ```creators```

Se esistono creators, i curatori del capitolo ```editors``` devono essere inseriti come contributor di tipo ```editor```. I curatori del libro ```book_editors```, devono essere inseriti nella proprietà ```[relatedItem](#20-relateditem)```. Non mappiamo invece i curatori della collana in cui è pubblicato il libro da cui il capitolo è tratto ```curators```.

=== "AMS Acta json"

    ```json
    {
    "type": "book_section",
    // Autori del capitolo, da mappare su creators
    "creators": [
        {
        "id": "marcusoliveira@unir.br",
        "affiliation": "Universidade Federal de Rondônia",
        "orcid": "0000-0002-9319-6094",
        "name": {
            "honourific": null,
            "given": "Marcus Vinícius Xavier",
            "family": "de Oliveira",
            "lineage": null
        }
        }
    ],
    // Editors del capitolo, in questo caso, da mappare su contributors di tipo editor
    "editors": [
        {
        "name": {
            "honourific": null,
            "lineage": null,
            "family": "Milani",
            "given": "Raffaele"
        },
        "affiliation": "Università di Bologna"
        }
    ],
    // Curatori della serie, non li mappiamo in DataCite
    "curators": [
        {
        "name": {
            "honourific": null,
            "lineage": null,
            "given": "Stefano",
            "family": "Ferrari"
        },
        "affiliation": "Università di Bologna",
        "id": "stefano.ferrari@unibo.it"
        }
    ],
    // Curatori del libro, da mappare su relatedItem
    "book_curators": [
        {
        "id": "laura.ricca2@unibo.it",
        "affiliation": "Università di Bologna",
        "name": {
            "family": "Ricca",
            "given": "Laura",
            "lineage": null,
            "honourific": null
        }
        }
    ],
    }
    ```

=== "DataCite xml"

    ```xml
    <creators>
        <creator>
            <creatorName>de Oliveira, Marcus Vinícius Xavier</creatorName>
            <givenName>Marcus Vinícius Xavier</givenName>
            <familyName>de Oliveira</familyName>
            <affiliation>Universidade Federal de Rondônia</affiliation>
            <nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0000-0002-9319-6094</nameIdentifier>
    </creators>
    <contributors>
        <contributor contributorType="Editor">
            <contributorName nameType="Personal">Milani, Raffaele</contributorName>
            <givenName>Raffaele</givenName>
            <familyName>Milani</familyName>
            <affiliation>Università di Bologna</affiliation>
        </contributor>
    </contributors>
    ```

### Monografie senza ```creators```

Mappiamo il campo ```editors``` su [Creators](#2-creator).

Il campo ```curators``` va invece mappato nella proprietà [relatedItem](#20-relateditem).

=== "AMS Acta json"

    ```json
    {
        "eprintid": 8364,
        "type": "monograph",
        // Curatori della monografia, da mappare in Creators
        "editors": [
        {
            "name": {
                "given": "Fulvia",
                "family": "Abbondante",
                "lineage": null,
                "honourific": null
            },
            "affiliation": "Università di Napoli “Federico II”"
            },
            {
            "affiliation": "Università di Napoli “Federico II”",
            "name": {
                "honourific": null,
                "lineage": null,
                "family": "Buono",
                "given": "Enrico"
            }
            },
            {
            "name": {
                "honourific": null,
                "family": "Di Donato",
                "given": "Flora",
                "lineage": null
            },
            "affiliation": "Università di Napoli “Federico II”"
            },
            {
            "affiliation": "Università di Napoli “Federico II”",
            "name": {
                "honourific": null,
                "given": "Giuseppe",
                "family": "Mastrominico",
                "lineage": null
            }
            },
        ]
        // Curatori della serie" 
        "curators": [
        {
            "orcid": "0000-0002-5321-7428",
            "name": {
                "honourific": null,
                "lineage": null,
                "family": "Faralli",
                "given": "Carla"
            },
            "affiliation": "Università di Bologna",
            "id": "carla.faralli@unibo.it"
            },
            {
            "id": "maria.mittica@uniurb.it",
            "orcid": "0000-0003-4352-4288",
            "name": {
                "honourific": null,
                "family": "Mittica",
                "given": "M. Paola",
                "lineage": null
            },
            "affiliation": "Università di Urbino"
        }
        ],
    }
    ```

=== "DataCite xml"

    ```xml
    <creators>
        <creator>
            <creatorName nameType="Personal">Abbondante, Fulvia</creatorName>
            <givenName>Fulvia</givenName>
            <familyName>Abbondante</familyName>
            <affiliation>Università di Napoli “Federico II”</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Buono, Enrico</creatorName>
            <givenName>Enrico</givenName>
            <familyName>Buono</familyName>
            <affiliation>Università di Napoli “Federico II”</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Di Donato, Flora</creatorName>
            <givenName>Flora</givenName>
            <familyName>Di Donato</familyName>
            <affiliation>Università di Napoli “Federico II”</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Mastrominico, Giuseppe</creatorName>
            <givenName>Giuseppe</givenName>
            <familyName>Mastrominico</familyName>
            <affiliation>Università di Napoli “Federico II”</affiliation>
        </creator>
    </creators>
    ```


Altro esempio, AMS Acta 5562

=== "Ams Acta json"

    ```json
    {
        "editors": [ // curatori del libro
        {
            "name": {
                "lineage": null,
                "given": "Flora",
                "family": "Di Donato",
                "honourific": null
            }
        },
        {
            "name": {
                "given": "Jean-Philippe",
                "family": "Dunand",
                "lineage": null,
                "honourific": null
            }
        },
        {
            "name": {
                "honourific": null,
                "lineage": null,
                "given": "Jean-Jacques",
                "family": "Aubert"
            }
        }
        ],
        "curators": [ // curatori della collana
        {
            "id": "carla.faralli@unibo.it",
            "affiliation": "Università di Bologna",
            "name": {
                "lineage": null,
                "family": "Faralli",
                "given": "Carla",
                "honourific": null
            },
            "orcid": null
        },
        {
            "id": "maria.mittica@uniurb.it",
            "affiliation": "Università di Urbino",
            "orcid": "0000-0003-4352-4288",
            "name": {
                "honourific": null,
                "given": "M. Paola",
                "family": "Mittica",
                "lineage": null
        }
        }
        ],
        "book_curators": [ // ignorare
        {
            "orcid": "0000-0003-4352-4288",
            "name": {
                "honourific": null,
                "lineage": null,
                "family": "Mittica",
                "given": "M. Paola"
            },
            "affiliation": "Università di Urbino",
            "id": "maria.mittica@uniurb.it"
        }
        ],
    }
    ```

### Monografie con autori

Creators sono gli autori della monografia (campo ```creators```).

I curatori della monografia (campo ```editors```) devono essere inseriti come contributor di tipo ```Editor```.

I curatori della serie (campo ```series_curators```) vanno mappati nella proprietà [relatedItem](#20-relateditem).


=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        // Autori della monografia
          "creators": [
        {
            "name": {
                "honourific": null,
                "family": "Giovannini",
                "given": "Federico",
                "lineage": null
            },
            "affiliation": null
            },
            {
            "affiliation": "ETH Zürich",
            "name": {
                "given": "Nicolàs",
                "family": "Palacios Crisòstomo",
                "lineage": null,
                "honourific": null
            }
            },
            {
            "affiliation": "Politecnico di Milano",
            "name": {
                "given": "Fabio",
                "family": "Iapaolo",
                "lineage": null,
                "honourific": null
            }
            },
            {
            "name": {
                "honourific": null,
                "family": "Blotta",
                "given": "Davide",
                "lineage": null
            },
            "affiliation": "Università degli studi di Urbino"
            },
            {
            "affiliation": "Università La Sapienza di Roma",
            "name": {
                "honourific": null,
                "given": "Edoardo",
                "family": "Biscossi",
                "lineage": null
            }
        },
        // Editors della monografia
        "editors": [
        {
            "id": "niccolo.cuppini2@unibo.it",
            "name": {
                "lineage": null,
                "family": "Cuppini",
                "given": "Niccolò",
                "honourific": null
            },
            "affiliation": "Scuola universitaria professionale della Svizzera italiana"
            },
            {
            "id": null,
            "affiliation": "ISCTE - University Institute of Lisbon",
            "name": {
                "family": "Pavoni",
                "given": "Andrea",
                "lineage": null,
                "honourific": null
            }
            },
            {
            "id": null,
            "name": {
                "honourific": null,
                "lineage": null,
                "given": "Simone",
                "family": "Tulumello"
            },
            "affiliation": "ICS-ULisboa - Universidade de Lisboa"
        }
        ],
        // Curatori della serie
        "series_curators": [
        {
        "name": {
            "honourific": null,
            "family": "Pirone",
            "given": "Maurilio",
            "lineage": null
        },
        "affiliation": "Università di Bologna",
        "id": "maurilio.pirone2@unibo.it"
        },
        {
        "affiliation": "Scuola universitaria professionale della Svizzera italiana",
        "name": {
            "honourific": null,
            "lineage": null,
            "given": "Niccolò",
            "family": "Cuppini"
        },
        "id": null
        },
        {
        "name": {
            "lineage": null,
            "given": "Mattia",
            "family": "Frapporti",
            "honourific": null
        },
        "affiliation": "Università di Bologna",
        "id": null
        },
        {
        "affiliation": null,
        "name": {
            "honourific": null,
            "family": "Benvegnù",
            "given": "Carlotta",
            "lineage": null
        },
        "id": null
        },
        {
        "name": {
            "honourific": null,
            "lineage": null,
            "family": "Milesi",
            "given": "Floriano"
        },
        "affiliation": null,
        "id": null
        }
        ],
    ],
    }
    ```

=== "DataCite xml"

    ```xml
    <creators>
        <creator>
            <creatorName nameType="Personal">Giovannini, Federico</creatorName>
            <givenName>Federico</givenName>
            <familyName>Giovannini</familyName>
        </creator>
        <creator>
            <creatorName nameType="Personal">Palacios Crisòstomo, Nicolàs</creatorName>
            <givenName>Nicolàs</givenName>
            <familyName>Palacios Crisòstomo</familyName>
            <affiliation>ETH Zürich</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Iapaolo, Fabio</creatorName>
            <givenName>Fabio</givenName>
            <familyName>Iapaolo</familyName>
            <affiliation>Politecnico di Milano</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Blotta, Davide</creatorName>
            <givenName>Davide</givenName>
            <familyName>Blotta</familyName>
            <affiliation>Università degli studi di Urbino</affiliation>
        </creator>
        <creator>
            <creatorName nameType="Personal">Biscossi, Edoardo</creatorName>
            <givenName>Edoardo</givenName>
            <familyName>Biscossi</familyName>
            <affiliation>Università La Sapienza di Roma</affiliation>
        </creator>
    </creators>
    <contributors>
        <contributor contributorType="Editor">
            <contributorName nameType="Personal">Cuppini, Niccolò</contributorName>
            <givenName>Niccolò</givenName>
            <familyName>Cuppini</familyName>
            <affiliation>Scuola universitaria professionale della Svizzera italiana</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName nameType="Personal">Pavoni, Andrea</contributorName>
            <givenName>Andrea</givenName>
            <familyName>Pavoni</familyName>
            <affiliation>ISCTE - University Institute of Lisbon</affiliation>
        </contributor>
        <contributor contributorType="Editor">
            <contributorName nameType="Personal">Tulumello, Simone</contributorName>
            <givenName>Simone</givenName>
            <familyName>Tulumello</familyName>
            <affiliation>ICS-ULisboa - Universidade de Lisboa</affiliation>
        </contributor>
    </contributors>
    ```

## 8. Date

Ora non è esposto. Occorre mappare le date disponibili su AMS Acta in questo modo

```
Pubblicato  			Issued 
Invio all’editore		Submitted 
Fine della stesura 		Created 
```

Aggiungiamo anche le seguenti date:

- data di fine embargo ```datetype="Available"``` se è specificata.
- data di deposito del record ```datetype="Accepted"```
- data di ultimo (oppure di ogni) aggiornamento del record ```datetype="Updated"```

Nell'archivio sono presenti record che contengono il metadato ```date_embargo``` e che non contengono ```date_embargo_retained``` (i record con l'embargo ancora attivo).

Sono presenti documenti che hanno solo ```date_embargo_retained``` e non ```date_embargo```. Si tratta dei record in cui l'embargo è scaduto e il file è stato reso disponibile.

Sono presenti documenti che hanno sia ```date_embargo``` che ```date_embargo_retained```. In questo caso, le due date sono sempre uguali.

La tabella riassume le mappature dei metadati.

| dateType          | metadato                                                |
|-------------------|---------------------------------------------------------|
| Issued            | ```"datetype": "published"```                           |
| Submitted         | ```"datetype": "submitted"```                           |
| Created           | ```"datetype": "completed"```                           |
| Accepted          | ```"datestamp"```                                       |
| Available         | ```"documents.date_embargo_retained"```, altrimenti ```"documents.date_embargo"``` |
| Updated           | ```"lastmod"```                                          |


=== "AMS Acta json" 

    ```json
    {
        "date": "2025-05-01",
        "date_type": "completed",
        "datestamp": "2025-05-23 14:10:15",
        "lastmod": "2025-07-04 10:12:12",
        "documents": [
            {
                "date_embargo_retained": "2025-06-30",
            }
        ]
    }
    ```

=== "DataCite xml"

    ```xml
    <dates>
        <date dateType="Created">2025-05-01</date>
        <date dateType="Accepted">2025-05-23</date>
        <date dateType="Available">2025-06-30</date>
        <date dateType="Updated">2025-07-04</date>
    </dates>
    ```

Le date, seguendo le indicazioni riportate [qui](https://www.w3.org/TR/NOTE-datetime) possono essere esposte nei seguenti formati:

```
YYYY
YYYY-MM
YYYY-MM-DD
YYYY-MM-DDTHH:MM:SSZ (i datestamp di AMS Acta sono già espressi in UTC)
```

## 9. Language

Il campo language è preso dalla lingua del primo file allegato.

=== "AMS Acta json" 

    ```json
    { 
        "documents": [
            {
            "pos": 1,
            "language": "it"
            }
        ]
    }
    ```
=== "DataCite xml"

    ```xml
    <language>it</language>
    ```

## 10. ResourceType

Vedi [sezione](resource-types.md)

## 11. AlternateIdentifier

AlternateIdentifierType è un campo libero. Come lista possiamo usare quella di [OpenAIRE](proprieta-openaire.md#5-alternate-identifier-r). Il DOI deve essere mappato con la proprietà [Identifier](#1-identifier).

<!--
```text
ARK
arXiv
DOI
Handle
ISBN
ISTC
PURL
URL
URN
w3id
Local accession number
RePEc ID
```
-->

Mappare il campo "ID alternativi". Oltre a questi, inserire anche la URL del record:

```xml
<alternateIdentifiers>
    <alternateIdentifier alternateIdentifierType="URL" >https://amsacta.unibo.it/id/eprint/7689/</alternateIdentifier>
</alternateIdentifiers>
```

In aggiunta, per le monografie aggiungere l'ISBN, quando è presente.

=== "AMS Acta json"

    ```json
    {
        "uri": "https://amsacta.unibo.it/id/eprint/8440",
        "type": "monograph",
        "monograph_type": "libro",
        "isbn": {
            "$numberLong": "9788854972001"
        }
        "alternateid": [
            {
            "idtype": "URL",
            "id": "http://www.contrastiva.it/wp/?page_id=115"
            }
     ],
    }
    ```
=== "DataCite xml"

    ```xml
    <alternateIdentifiers>
        <alternateIdentifier alternateIdentifierType="URL">https://amsacta.unibo.it/id/eprint/8440</alternateIdentifier>
        <alternateIdentifier alternateIdentifierType="ISBN">9788854972001</alternateIdentifier>
        <alternateIdentifier alternateIdentifierType="URL">http://www.contrastiva.it/wp/?page_id=115</alternateIdentifier>
    </alternateIdentifiers>
    ```

## 12. RelatedIdentifiers

Aggiornare la lista dei relatedIdentifierType.

| Stato     | relatedIdentifierType |
|-----------|-----------------------|
| Esistente | ARK                   |
| Esistente | arXiv                 |
| Esistente | bibcode               |
| Nuovo     | CSTR                  |
| Esistente | DOI                   |
| Esistente | EAN13                 |
| Esistente | EISSN                 |
| Esistente | Handle                |
| Nuovo     | IGSN                  |
| Esistente | ISBN                  |
| Esistente | ISSN.                 |
| Esistente | ISTC                  |
| Esistente | LISSN                 |
| Esistente | LSID                  |
| Esistente | PMID                  |
| Esistente | PURL                  |
| Nuovo     | RRID                  |
| Esistente | UPC                   |
| Esistente | URL                   |
| Esistente | URN                   |
| Nuovo     | w3id                  |

Il campo non è esposto. Mappare il campo risorse collegate

```xml
<relatedIdentifiers>
    <relatedIdentifier relatedIdentifierType="DOI" relationType="IsSupplementTo">10.1234/related-doi</relatedIdentifier>
<relatedIdentifiers>
```

Mappare i singoli file, con la loro URL, con il relationType="HasPart".
```xml
<relatedIdentifiers>
    <relatedIdentifier relatedIdentifierType="URL" relationType="HasPart">https://amsacta.unibo.it/1234/file.pdf</relatedIdentifier>
</relatedIdentifiers>
```

Mappare le nuove o le precedenti versioni con relationType="IsNewVersionOf" o "IsPreviousVersionOf".

```xml
<relatedIdentifiers>
    <relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.1234/old-version-doi</relatedIdentifier>
    <relatedIdentifier relatedIdentifierType="DOI" relationType="IsPreviousVersionOf">10.1234/new-version-doi</relatedIdentifier>       
</relatedIdentifiers>
```

Per i capitoli di libro, mappare la relazione del capitolo con il libro con relationType="IsPublishedIn"

```xml
<relatedIdentifiers>
    <relatedIdentifier relatedIdentifierType="ISBN" relationType="IsPublishedIn">0-12-345678-1</relatedIdentifier>
</relatedIdentifiers>
```
Per i libri in collana, mappare la relazione del libro con la collana con relationType="IsPartOf" (o "IsCollectedBy")

```xml
<relatedIdentifiers>
    <relatedIdentifier relatedIdentifierType="ISSN" relationType="IsPartOf">0000-1234</relatedIdentifier>
</relatedIdentifiers>
```

Aggiornare la lista dei ```relationType```. Ecco la lista

| Stato     | relationType          | Etichetta EN                             | Etichetta IT                                      |
|-----------|-----------------------|------------------------------------------|---------------------------------------------------|
| Esistente | IsCitedBy             | This upload is cited by                  | Questo contributo è citato da                     |
| Esistente | Cites                 | This upload cites                        | Questo contributo cita                            |
| Esistente | IsSupplementTo        | This upload is supplement to             | Questo contributo è un supplemento di             |
| Esistente | IsSupplementedBy      | This upload is supplemented by           | Questo contributo ha come supplemento             |
| Esistente | IsContinuedBy         | This upload is continued by              | Questo contributo è continuato da                 |
| Esistente | Continues             | This upload continues                    | Questo contributo è una continuazione di          |
| Nuovo     | IsDescribedBy         | This upload is described by              | Questo contributo è descritto da                  |
| Nuovo     | Describes             | This upload describes                    | Questo contributo descrive                        |
| Esistente | HasMetadata           | This upload has additional metadata in   | Questo contributo ha ulteriori metadati in        |
| Esistente | IsMetadataFor         | This upload is additional metadata for   | Questo contributo è un ulteriore metadato di      |
| Nuovo     | HasVersion            | This upload has a version in             | Questo contributo ha una versione in              |
| Nuovo     | IsVersionOf           | This upload is a version of              | Questo contributo è una versione di               |
| Esistente | IsNewVersionOf        | This upload is a new version of          | Questo contributo è una nuova versione di         |
| Esistente | IsPreviousVersionOf   | This upload is a previous version of     | Questo contributo è una precedente versione di    |
| Esistente | IsPartOf              | This upload is part of                   | Questo contributo è parte di                      |
| Esistente | HasPart               | This upload includes                     | Questo contributo include                         |
| Nuovo     | IsPublishedIn         | This upload is published in              | Questo contributo è pubblicato in                 |
| Esistente | IsReferencedBy        | This upload is referenced by             | Un riferimento a questo contributo è contenuto in |
| Esistente | References            | This upload references                   | Questo contributo contiene riferimenti a          |
| Esistente | IsDocumentedBy        | This upload is documented by             | Questo contributo è documentato da                |
| Esistente | Documents             | This upload supplies documentation about | Questo contributo documenta                       |
| Esistente | IsCompiledBy          | This upload is compiled by               | Questo contributo è compilato o creato da         |
| Esistente | Compiles              | This upload compiles                     | Questo contributo compila o crea                  |
| Esistente | IsVariantFormOf       | This upload is a variant form of         | Questo contributo è una variazione di             |
| Esistente | IsOriginalFormOf      | This upload is the original form of      | Questo contributo è l'originale di                |
| Esistente | IsIdenticalTo         | This upload is identical to              | Questo contributo è identico a                    |
| Esistente | IsReviewedBy          | This upload is reviewed by               | Questo contributo è recensito da                  |
| Esistente | Reviews               | This upload reviews                      | Questo contributo recensisce                      |
| Esistente | IsDerivedFrom         | This upload is derived from              | Questo contributo è derivato da                   |
| Esistente | IsSourceOf            | This upload is source of                 | Questo contributo è una fonte di                  |
| Nuovo     | IsRequiredBy          | This upload is required by               | Questo contributo è richiesto da                  |
| Nuovo     | Requires              | This upload requires                     | Questo contributo richiede                        |
| Nuovo     | IsObsoletedBy         | This upload is obsoleted by              | Questo contributo è reso obsoleto da              |
| Nuovo     | Obsoletes             | This upload obsoletes                    | Questo contributo rende obsoleto                  |
| Nuovo     | IsCollectedBy         | This upload is collected by              | Questo contributo è raccolto attraverso           |
| Nuovo     | Collects              | This upload collects                     | Questo contributo raccoglie                       |
| Nuovo     | IsTranslationOf       | This upload is a translation of          | Questo contributo è una traduzione di             |
| Nuovo     | HasTranslation        | This upload has a translation            | Questo contributo è tradotto in                   |

Esempio di mappatura dei ```relatedId``` e dei singoli file.

=== "AMS Acta json"

    ```json
    {
        
        "relatedid": [
        {
        "idtype": "DOI",
        "id": "https://doi.org/10.6092/unibo/amsacta/8307",
        "relationtype": "IsNewVersionOf"
        },
        {
        "relationtype": "IsSupplementTo",
        "id": "https://doi.org/10.1080/17452759.2025.2526032",
        "idtype": "DOI"
        }
        "documents": [
            {
            "uri": "https://amsacta.unibo.it/id/document/24241010",
            },
    }
    ```

=== "DataCite xml"

    ```xml
    <relatedIdentifiers>
        <relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.6092/unibo/amsacta/8307</relatedIdentifier>
        <relatedIdentifier relatedIdentifierType="DOI" relationType="IsSupplementTo">10.1080/17452759.2025.2526032</relatedIdentifier>
        <relatedIdentifier relatedIdentifierType="URL" relationType="HasPart">https://amsacta.unibo.it/id/document/24241010</relatedIdentifier>
    </relatedIdentifiers>       
    ```

Per i capitoli di libro, oltre a ISBN e link ai fulltext

=== "AMS Acta json"

    ```json
    "type": "book_section",
    "isbn": {
        "$numberLong": "9788854971844"
    },
    "issn": "2035-553X"
    ```
=== "DataCite xml"

    ```xml
    <relatedIdentifiers>
        <relatedIdentifier relatedIdentifierType="ISBN" relationType="IsPublishedIn">9788854971844</relatedIdentifier>
        <relatedIdentifier relatedIdentifierType="ISSN" relationType="IsPartOf">2035-553X</relatedIdentifier>
    </relatedIdentifiers>
    ```

Per i libri in collana, oltre a ISBN e link ai fulltext

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "issn": "2724-2583"
    }
    ```

=== "DataCite xml"

    ```xml
    <relatedIdentifiers>
        <relatedIdentifier relatedIdentifierType="ISSN" relationType="IsPartOf">2724-2583</relatedIdentifier>
    </relatedIdentifiers>
    ```

## 13. Size

Per ogni allegato, specificare la dimensione in byte.

=== "AMS Acta json" 
    ```json
    "documents": [
    {
        "files": [
        {
            "filesize": 34649250,
        }
        ],
    }    
    ]
    ```
    
=== "Datacite xml"
    ```xml
    <sizes>
        <size>34649250</size>
    </sizes>
    ```

Mappare il campo numero di pagine come

=== "AMS Acta json" 
    ```json
    {
        "pages": 78
    }
    ```

=== "Datacite xml"
    ```xml
    <sizes>
        <size>78 pages</size>
    </sizes>
    ```

## 14. Format

Per ogni allegato, specificare il MIME type.

=== "AMS Acta json" 
    ```json
    "documents": [
    {
      "files": [
        {
          "mime_type": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
        }
        {
          "mime_type": "application/zip",
        }
    }    
    ]
    ```
=== "Datacite xml"
    ```xml
    <formats>
        <format>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</format>
        <format>application/zip</format>
    </formats>
    ```

## 15. Version

Non abbiamo il metadato e quindi non lo esponiamo. Per le versioni precedenti e successive usiamo [RelatedIdentifier](#12-relatedidentifiers) con relationType="IsNewVersionOf" e "IsPreviousVersionOf".

## 16. Rights

Per ogni allegato, specificare la licenza. Usare gli [identificativi SPDX](https://spdx.org/licenses/). La lingua ```xml:lang``` è la lingua del file corrispondente.

=== "AMS Acta json" 
    ```json
    "documents": [
    {
      "language": "en",
      "license": "cc_by_4"
    }
    {
      "language": "it",
      "license": "studio_ricerca"
    }    
    ]
    ```

=== "Datacite xml"
    ```xml
    <rightsList>
        <rights xml:lang="en" schemeURI="https://spdx.org/licenses/" rightsIdentifierScheme="SPDX" rightsIdentifier="CC-BY-4.0" rightsURI="https://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International</rights>
        <rights xml:lang="it">Consenti di salvare e stampare il contributo per scopi di studio personale, di ricerca e d'insegnamento.</rights>
    </rightsList>
    ```

Per le licenze personalizzate, usare il testo completo della licenza. Per le licenze standard, occorre mappare le etichette di AMS Acta con le etichette SPDX.

| Licenza AMS Acta      | SPDX ID         | LINK         |
|-----------------------|-----------------|--------------|
| cc_by_4               | CC-BY-4.0       |              |
| cc_by                 | CC-BY-3.0       |              |
| cc_by_nc              | CC-BY-NC-3.0    |              |
| cc_by_nc_4            | CC-BY-NC-4.0    |              |
| cc_by_nc_nd           | CC-BY-NC-ND-3.0 |              |
| cc_by_nc_nd_4         | CC-BY-NC-ND-4.0 |              |
| cc_by_nc_sa           | CC-BY-NC-SA-3.0 |              |
| cc_by_nc_sa_4         | CC-BY-NC-SA-4.0 |              |
| cc_by_nd              | CC-BY-ND-3.0    |              |
| cc_by_nd_4            | CC-BY-ND-4.0    | |
| cc_by_sa              | CC-BY-SA-3.0    | |
| cc_by_sa_4            | CC-BY-SA-4.0    | |
| cc_zero_1             | CC0-1.0         | |
| cc_by_nc_sa_igo       | CC-BY-NC-SA-3.0-IGO | https://creativecommons.org/licenses/by-nc-sa/3.0/igo/ |
| gpl_3                 | GPL-3.0        | https://www.gnu.org/licenses/gpl-3.0.html |
| mit                   | MIT            | https://opensource.org/licenses/mit |




## 17. Descriptions

Mappare il campo abstract. Il campo della lingua viene preso dalla lingua del primo file allegato.

=== "AMS Acta json" 
    ```json
    {
        "abstract": "Vengono trattati i fondamenti generali di energetica e i principi di funzionamento e gli schemi di realizzazione degli impianti non convenzionali, (nucleari a fissione e a fusione), e da fonti rinnovabili, (solare, idraulico, eolico, biomasse, geotermico), per la produzione di energia e i sistemi avanzati di conversione energetica, (celle a combustibile, fotovoltaica, magnetofluidodinamica, termoelettrica diretta, termoelettronica).\r\nVengono forniti i criteri generali di analisi degli investimenti e dei profitti per l'ottimizzazione dei sistemi impiantistici e i criteri di economia energetica degli impianti di produzione e conversione energetica.\r\nSi esaminano i criteri tecnici ed economici degli interventi per il risparmio e il recupero energetico e l'impiego di rifiuti e inquinanti per la produzione di combustibili pregiati.",
        "documents": [
            {
            "language": "it",
            "pos": 1,
            }
        ]
    }
    ```
=== "DataCite xml"
    ```xml
    <descriptions>
        <description xml:lang="it" descriptionType="Abstract">Vengono trattati i fondamenti generali di energetica e i principi di funzionamento e gli schemi di realizzazione degli impianti non convenzionali, (nucleari a fissione e a fusione), e da fonti rinnovabili, (solare, idraulico, eolico, biomasse, geotermico), per la produzione di energia e i sistemi avanzati di conversione energetica, (celle a combustibile, fotovoltaica, magnetofluidodinamica, termoelettrica diretta, termoelettronica).\r\nVengono forniti i criteri generali di analisi degli investimenti e dei profitti per l'ottimizzazione dei sistemi impiantistici e i criteri di economia energetica degli impianti di produzione e conversione energetica.\r\nSi esaminano i criteri tecnici ed economici degli interventi per il risparmio e il recupero energetico e l'impiego di rifiuti e inquinanti per la produzione di combustibili pregiati.</description>
    </descriptions>
    ```

## 18. GeoLocations

Per ora esponiamo solo la sottoproprietà geoLocationPlace (testo libero).

=== "AMS Acta json"

    ```json
    "geolocplace": [
        {
        "place": "Bologna, Italy"
        }
    ],
    ```

=== "DataCite xml"

    ```xml
    <geoLocations>
    <geoLocation>
        <geoLocationPlace>Disko Bay</geoLocationPlace>
    </geoLocation>
    </geoLocations>
    ```

## 19. FundingReferences

Versione che possiamo mappare con i metadati attualmente disponibili, in attesa di capire come moltiplicare il campo finanziamento.

=== "AMS Acta"

    ```json
    "fundingprogramme": "H2020",
    "funder": "EC",
    "jurisdiction": "EU",
    "projectid": 101016503,
    "projectname": "In Silico World: Lowering barriers to ubiquitous adoption of In Silico Trials"
    ```

=== "DataCite xml"

    ```xml
    <fundingReferences>
    <fundingReference>
        <funderName>EC</funderName>
        <awardNumber>101016503</awardNumber>
        <awardTitle>In Silico World: Lowering barriers to ubiquitous adoption of In Silico Trials</awardTitle>
        </fundingReference>
    </fundingReferences>
    ```

Come dovrebbe essere

=== "DataCite xml"

    ```xml
    <fundingReferences>
    <fundingReference>
        <funderName>European Commission</funderName>
        <funderIdentifier funderIdentifierType="Crossref Funder ID">https://doi.org/10.13039/501100000780</funderIdentifier>
        <awardNumber awardURI="https://cordis.europa.eu/project/rcn/100180_en.html">282625</awardNumber>
        <awardTitle>MOTivational strength of ecosystem services and alternative ways to express the value of BIOdiversity</awardTitle>
        </fundingReference>
    <fundingReference>
        <funderName>European Commission</funderName>
        <funderIdentifier funderIdentifierType="Crossref Funder ID">https://doi.org/10.13039/501100000780</funderIdentifier>
        <awardNumber awardURI="https://cordis.europa.eu/project/rcn/100603_en.html">284382</awardNumber>
        <awardTitle>Institutionalizing global genetic-resource commons. Global Strategies for accessing and using essential public knowledge assets in the life sciences</awardTitle>
    </fundingReference>
    </fundingReferences>
    ```

Metadato che non serve per DataCite ma servirà per [Openaire 4](proprieta-openaire.md#4-fundingreferences-ma)

| Metadato di AMS ACTA              | Sottoproprietà Openaire 4 |
|-----------------------------------|---------------------------|
| eprint_fieldname_fundingprogramme | fundingStream             |


Predisporre i metadati mancanti

- funderIdentifierType (lista controllata: Crossref Funder ID, ROR, ISNI)
- funderIdentifier
- awardURI

Attualmente, prendiamo la lista dei progetti attraverso le [API di Openaire per EPrints](https://graph.openaire.eu/docs/apis/dspace-eprints-api).

Questa API non espone il ```funderIdentifier``` e l'```awardURI```.

Per i progetti della Commissione Europea, ```awardURI``` può essere ricostruito nella forma ```https://cordis.europa.eu&project/ID/<projectid>```, oppure ```https://doi.org/10.3030/10.<projectID>```.

Il Funder Identifier si potrebbe prendere da una tabella interna, o dalle API del [Crossref Funder registry](https://www.crossref.org/services/funder-registry/).

Ad oggi, OpenAIRE fornisce metadati per diversi funders (non solo European Commission). Valutiamo se aggiungere la possibilità di avere la ricerca automatica del progetto anche per altri enti finanziatori.

Il campo dovrebbe essere duplicabile nella maschera di inserimento. Il campo deve essere duplicabile per diverse tipologie di finanziamento. Idealmente, si potrebbe rimuovere la scelta del tipo di finanziamento prima dell'inserimento del progetto. Ad esempio, come avviene già per IRIS.

## 20. RelatedItem 

Questo metadato è più preciso di RelatedIdentifier. Possiamo usarlo per i capitoli di libro per inserire gli ISBN, o per i libri per inserire gli ISSN della collana.

I metadati da usare sono i seguenti

### Estratto da libro

Mappare la relazione del capitolo con il libro. I metadati da utilizzare sono i seguenti.

=== "AMS Acta json"

    ```json
    {
        "type": "book_section",
        "isbn": {
        "$numberLong": "9788854971844"
        },
        "book_curators": [
            {
            "name": {
                "given": "Carla",
                "family": "Faralli",
            },
            "orcid": "0000-0002-5321-7428",
            "affiliation": "Università di Bologna",
            "id": "carla.faralli@unibo.it"
            },
            {
            "name": {
                "family": "Mittica",
                "given": "M. Paola",
            },
            "orcid": "0000-0003-4352-4288",
            "affiliation": "Università di Urbino",
            "id": "maria.mittica@uniurb.it"
            }
        ],
        "book_title": "Vol. 18/2025",
        "pagerange": "1-23",
        "publisher": "Italian Society for Law and Literature (ISLL)",
    }
    ```

=== "DataCite xml"

    ```xml
        <relatedIdentifiers>
            <relatedIdentifier relatedIdentifierType="ISBN" relationType="IsPublishedIn">9788854971844</relatedIdentifier>
        </relatedIdentifiers>
        <relatedItems>
            <relatedItem relationType="IsPublishedIn" relatedItemType="Book">
                <relatedItemIdentifier relatedItemIdentifierType="ISBN">97834567823421</relatedItemIdentifier>
                <contributors>             <!-- Aggiungere i curatori del libro come contributors di tipo Editor (book_curators?) -->
                    <contributor contributorType="Editor">
                        <contributorName nameType="Personal">Faralli, Carla</contributorName>
                        <givenName>Faralli</givenName>
                        <familyName>Carla</familyName>
                    </contributor>
                        <contributor contributorType="Editor">
                        <contributorName nameType="Personal">M. Paola, Mittica</contributorName>
                        <givenName>Mittica</givenName>
                        <familyName>M. Paola</familyName>
                    </contributor>
                </contributors>
                <titles>
                    <title>Vol. 18/2025</title>
                </titles>
                <firstPage>1</firstPage>
                <lastPage>23</lastPage>
                <publisher>Italian Society for Law and Literature (ISLL)</publisher>
            </relatedItem>
        </relatedItems>
    ```

### Documento relativo a convegno o altro evento

=== "AMS Acta json"

    ```json
    {
        "type": "conference_item",
        "event_title": "Simposio 2G-C",
        "event_dates": "26/06/2025"
    }
    ```

=== "DataCite xml"

    ```xml
    <relatedItems>
        <relatedItem relationType="IsPartOf" relatedItemType="Event">
            <titles>
                <title>Titolo dell'evento</title> <!--- event_title -->
            </titles>
            <publicationYear>2025</publicationYear> <!-- event_dates -->
        </relatedItem>
    </relatedItems>
    ```

### Monografie

Per i libri in collana, mappare la relazione del libro con la collana.

Questi sono i metadati da utilizzare.

=== "AMS Acta json"
   
    ```json
    {
        "monograph_type": "libro",
        "series": "I Quaderni di Into the Black Box",
        "series_number": 6,
        "series_curators": [
            {
            "name": {
                "honourific": null,
                "family": "Pirone",
                "given": "Maurilio",
                "lineage": null
            },
            "affiliation": "Università di Bologna",
            "id": "maurilio.pirone2@unibo.it"
            },
            {
            "affiliation": "Scuola universitaria professionale della Svizzera italiana",
            "name": {
                "honourific": null,
                "lineage": null,
                "given": "Niccolò",
                "family": "Cuppini"
            },
            "id": null
            }
        ],
    }
    ```

=== "DataCite xml"

    ```xml
    <relatedIdentifiers>              <!-- Aggiungere l'ISSN della collana come relatedIdentifier -->
        <relatedIdentifier relatedIdentifierType="ISSN" relationType="IsPublishedIn">0000-1234</relatedIdentifier>
    </relatedIdentifiers>
    <relatedItems>
        <relatedItem relationType="IsPartOf" relatedItemType="Collection">
            <relatedItemIdentifier relatedItemIdentifierType="ISSN">0000-1234</relatedItemIdentifier>
            <contributors>             <!-- Aggiungere i curatori della collana, se esistono -->
                <contributor contributorType="Editor"> <!-- series_curators -->
                <contributorName nameType="Personal">Pirone, Maurilio</contributorName>
                <givenName>Maurilio</givenName>
                <familyName>Pirone</familyName>
                </contributor>
                <contributor contributorType="Editor"> <!-- series_curators -->
                <contributorName nameType="Personal">Cuppini, Niccolò</contributorName>
                <givenName>Niccolò</givenName>
                <familyName>Cuppini</familyName>
                </contributor>
            </contributors>
            <titles>
                <title>I Quaderni di Into the Black Box</title> <!-- series -->
            </titles>
            <number numberType="Other">6</number> <!-- Numero all'interno della collana series_number -->
        </relatedItem>
    </relatedItems>
    ```