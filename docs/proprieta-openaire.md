# Proprietà di Openaire

La descrizione delle proprietà si trova [qui](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/stable/application_profile.html).

# 0. Resource

Gli schemi e i namespace utilizzati devono essere dichiarati in questo modo

=== "OpenAIRE xml"

    ```xml
    <oaire:resource xmlns:oaire="http://namespace.openaire.eu/schema/oaire/" 
                    xmlns:rdf="http://www.w3.org/1999/02/22-rdf-syntax-ns#"
                    xmlns:dc="http://purl.org/dc/elements/1.1/"
                    xmlns:dcterms="http://purl.org/dc/terms/"
                    xmlns:datacite="http://datacite.org/schema/kernel-4"
                    xmlns:vc="http://www.w3.org/2007/XMLSchema-versioning"
                    xsi:schemaLocation="http://namespace.openaire.eu/schema/oaire/ https://www.openaire.eu/schema/repo-lit/4.0/openaire.xsd"
                    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    ```

# 1. Title (M)

Si utilizza il campo ```title```. La lingua viene presa dalla lingua del primo file allegato. Il ROR è stato aggiunto nel sito di sviluppo.

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

=== "OpenAIRE xml"
  ```xml
  <datacite:title xml:lang="it" >Titolo del contributo</datacite:title>
  ```

Al momento il titolo non è duplicabile. Non utilizziamo l'attributo ```titleType```.

# 2. Creator (M)

I creators e le sottoproprietà sono presi dal campo ```creators```. Il ROR non è ancora previsto dallo schema di OpenAIRE nella versione stabile 4.0.1. La [beta di sviluppo](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/latest/field_creator.html) include già il ROR. Possiamo già includerlo, dato che abbiamo già il metadato per [DataCite](proprieta-datacite.md#2-creator)? Chiediamo a OpenAIRE?

Mappare editors quando non ci sono creator |||||||||||||||||||||||||||||

=== "AMS Acta json"

    ```json
    "creators": [
        {
        "id": "vito.baldassarro@unibo.it",
        "affiliation": "University of Bologna",
        "orcid": "0000-0003-1020-4261",
        "ror": "01111rn36",
        "name": {
            "honourific": null,
            "lineage": null,
            "family": "Baldassarro",
            "given": "Vito Antonio"
        }
        },
        {
        "orcid": "0009-0004-0124-1110",
        "ror": "00pg6eq24",
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

=== "OpenAIRE xml"
    ```xml
    <datacite:creators>
        <datacite:creator>
            <datacite:creatorName nametype="personal">Baldassarro, Vito Antonio</datacite:creatorName>
            <datacite:givenName>Baldassarro</datacite:givenName>
            <datacite:familyName>Vito Antonio</datacite:familyName>
            <datacite:affiliation>University of Bologna</datacite:affiliation>
            <datacite:nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0000-0002-9494-5384</datacite:nameIdentifier>
        </datacite:creator>
        <datacite:creator>
            <datacite:creatorName>Brassart, Quentin</datacite:creatorName>
            <datacite:givenName>Quentin</datacite:givenName>
            <datacite:familyName>Brassart</datacite:familyName>
            <datacite:affiliation>Université de Strasbourg</datacite:affiliation>
            <datacite:nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0009-0004-0124-1110</datacite:nameIdentifier>
        </datacite:creator>
    </datacite:creators>
    ```

=== "OpenAIRE 4.1 xml"
    ```xml
    <datacite:creators>
        <datacite:creator>
            <datacite:creatorName>Baldassarro, Vito Antonio</datacite:creatorName>
            <datacite:givenName>Baldassarro</datacite:givenName>
            <datacite:familyName>Vito Antonio</datacite:familyName>
            <datacite:affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">University of Bologna</datacite:affiliation>
            <datacite:nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0000-0002-9494-5384</datacite:nameIdentifier>
        </datacite:creator>
        <datacite:creator>
            <datacite:creatorName>Brassart, Quentin</datacite:creatorName>
            <datacite:givenName>Quentin</datacite:givenName>
            <datacite:familyName>Brassart</datacite:familyName>
            <datacite:affiliation affiliationIdentifier="https://ror.org/00pg6eq24" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">Université de Strasbourg</datacite:affiliation>
            <datacite:nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID" >0009-0004-0124-1110</datacite:nameIdentifier>
        </datacite:creator>
    </datacite:creators>
    ```

# 3. Contributor (MA)

Il metadato da mappare è ```contributors```. La versione di sviluppo include già il ROR dell'affiliazione.

=== "AMS Acta json"

    ```json
      "contributors": [
        {
          "affiliation": "Università di Bologna",
          "ror": "https://ror.org/01111rn36",
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
          "ror": "https://ror.org/01111rn36",
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

=== "OpenAIRE xml"
    ```xml
    <datacite:contributors>
        <datacite:contributor contributorType="DataManager">
            <datacite:contributorName nameType="Personal">Katarina, Lučić</datacite:contributorName>
            <datacite:givenName>Lučić</datacite:givenName>
            <datacite:familyName>Katarina</datacite:familyName>
            <datacite:nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0009-0008-0919-301X</datacite:nameIdentifier>
            <datacite:affiliation>Università di Bologna</datacite:affiliation>
        </datacite:contributor>
        <datacite:contributor contributorType="ContactPerson">
            <datacite:contributorName nameType="Personal">Iezzi, Adriana</datacite:contributorName>
            <datacite:givenName>Adriana</datacite:givenName>
            <datacite:familyName>Iezzi</datacite:familyName>
            <datacite:nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0000-0001-8803-8940</datacite:nameIdentifier>
            <datacite:affiliation>Università di Bologna</datacite:affiliation>
        </datacite:contributor>
    </datacite:contributors>
    ```

=== "OpenAIRE 4.1 xml"
    ```xml
    <datacite:contributors>
        <datacite:contributor contributorType="DataManager">
            <datacite:contributorName nameType="Personal">Katarina, Lučić</datacite:contributorName>
            <datacite:givenName>Lučić</datacite:givenName>
            <datacite:familyName>Katarina</datacite:familyName>
            <datacite:nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0009-0008-0919-301X</datacite:nameIdentifier>
            <datacite:affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">Università di Bologna</datacite:affiliation>
        </datacite:contributor>
        <datacite:contributor contributorType="ContactPerson">
            <datacite:contributorName nameType="Personal">Iezzi, Adriana</datacite:contributorName>
            <datacite:givenName>Adriana</datacite:givenName>
            <datacite:familyName>Iezzi</datacite:familyName>
            <datacite:nameIdentifier schemeURI="https://orcid.org/" nameIdentifierScheme="ORCID">0000-0001-8803-8940</datacite:nameIdentifier>
            <datacite:affiliation affiliationIdentifier="https://ror.org/03efmqc40" affiliationIdentifierScheme="ROR" schemeURI="https://ror.org">Università di Bologna</datacite:affiliation>
        </datacite:contributor>
    </datacite:contributors>
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
Translator    (presente in DataCite ma non in OpenAIRE)
WorkPackageLeader
Other
```

Mantenere nella lista

```
Funder
```

Nello schema di OpenAIRE non c'è ```Translator```, ma lo aggiungerei lo stesso (forse dovremmo segnalarlo?). Cosa succede ad OpenAIRE 4 se usiamo questo valore?

<!--
L'[ultima versione (ancora in beta)](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/latest/field_contributor.html) introduce anche questi ruoli dalla National Information Standards Organization (NISO). Valutare se aggiungerli o attendere.

```
Conceptualization
FormalAnalysis
FundingAcquisition
Investigation
Methodology
Validation
Visualization
```
-->

I curatori del volume e i curatori della collana devono essere inseriti come contributor di tipo ```Editor```.

# 4. FundingReferences (MA)

Versione che possiamo mappare con i metadati attualmente disponibili, in attesa di capire come moltiplicare il campo finanziamento, e come aggiungere i campi mancanti.

=== "AMS Acta"

    ```json
    "fundingprogramme": "H2020",
    "funder": "EC",
    "jurisdiction": "EU",
    "projectid": 101016503,
    "projectidvalid": "TRUE",
    "projecttype": "eu",
    "projectname": "In Silico World: Lowering barriers to ubiquitous adoption of In Silico Trials",
    "projectacronym": "ISW"
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:fundingReferences>
      <oaire:fundingReference>
      <oaire:funderName>EC</oaire:funderName>
      <oaire:fundingStream>H2020</oaire:fundingStream>
      <oaire:awardNumber>101016503</oaire:awardNumber>
      <oaire:awardTitle>In Silico World: Lowering barriers to ubiquitous adoption of In Silico Trials</oaire:awardTitle>
      </oaire:fundingReference>
    </oaire:fundingReferences>
    ```

Come dovrebbe essere esposto.

=== "OpenAIRE xml"

    ```xml
    <oaire:fundingReferences>
      <oaire:fundingReference>
        <oaire:funderName>European Commission</oaire:funderName>
        <oaire:funderIdentifier funderIdentifierType="Crossref Funder ID">https://doi.org/10.13039/501100000780</oaire:funderIdentifier>
        <oaire:awardNumber awardURI="https://cordis.europa.eu/project/rcn/100180_en.html">101016503</oaire:awardNumber>
        <oaire:awardTitle>In Silico World: Lowering barriers to ubiquitous adoption of In Silico Trials</awardTitle>
        <oaire:fundingStream>H2020</oaire:fundingStream>
    </oaire:fundingReferences>
    ```

Mappatura dei metadati di AMS Acta con le sottoproprietà di OpenAIRE

| Metadato di AMS ACTA  | Sottoproprietà OpenAIRE |
|-----------------------|-------------------------|
| projectid             |  awardNumber            |
| funder                |  funderName             |
| projectname           |  awardTitle             |
| fundingprogramme      |  fundingStream          |

Predisporre i metadati mancanti

- funderIdentifierType (lista controllata: Crossref Funder ID, ROR, ISNI)
- funderIdentifier
- awardURI

Attualmente, prendiamo la lista dei progetti attraverso le [API di Openaire per EPrints](https://graph.openaire.eu/docs/apis/dspace-eprints-api).

Questa API non espone il ```funderIdentifier``` e l'```awardURI```.

Per i progetti della Commissione Europea, ```awardURI``` può essere ricostruito nella forma ```https://cordis.europa.eu&project/ID/<projectid>```, oppure ```https://doi.org/10.3030/10.<projectID>```.

## Evolutive future

Il Funder Identifier si potrebbe prendere da una tabella interna, o dalle API del [Crossref Funder registry](https://www.crossref.org/services/funder-registry/).

Ad oggi, OpenAIRE fornisce metadati per diversi funders (non solo European Commission). Valutiamo se aggiungere la possibilità di avere la ricerca automatica del progetto anche per altri enti finanziatori.

Il campo dovrebbe essere duplicabile nella maschera di inserimento. Il campo deve essere duplicabile per diverse tipologie di finanziamento. Idealmente, si potrebbe rimuovere la scelta del tipo di finanziamento prima dell'inserimento del progetto. Ad esempio, come avviene già per IRIS.

# 5. Alternate Identifier (R)

Il DOI non deve essere mappato qui, ma nella sezione [Resource Identifier](#14-resource-identifier-m). Aggiornare la lista degli alternateIdentifierType. Per la lista degli alternate idetifier type vedi la lista di [DataCite](proprieta-datacite.md#11-alternateidentifier).

Aggiungere alla lista degli identifcativi alternativi ```Local accession number``` e ```Scopus ID```.

<!--
```text
ARK
arXiv
bibcode   
DOI
EAN13     
EISSN     
Handle
IGSN
ISBN
ISSN
ISTC
LISSN
LSID
PISSN
PMID
PURL
UPC
URL
URN
WOS
```

```
w3id
Local accession number
RePEc ID
```
-->

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
    <datacite:alternateIdentifiers>
        <adatacite:lternateIdentifier alternateIdentifierType="URL">https://amsacta.unibo.it/id/eprint/8440</datacite:alternateIdentifier>
        <datacite:alternateIdentifier alternateIdentifierType="ISBN">9788854972001</datacite:alternateIdentifier>
        <datacite:alternateIdentifier alternateIdentifierType="URL">http://www.contrastiva.it/wp/?page_id=115</datacite:alternateIdentifier>
    </alternateIdentifiers>
    ```

# 6. Related Identifier (R)

La lista controllata è la stessa usata per [DataCite](proprieta-datacite.md#12-relatedidentifiers), senza gli identificativi specificati sotto.
<!--
```text
ARK
arXiv
bibcode   
DOI
EAN13     
EISSN     
Handle
IGSN
ISBN
ISSN
ISTC
LISSN
LSID
PISSN
PMID
PURL
UPC
URL
URN
WOS
```

La lista delle relazioni è

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
-->
Le seguenti relazioni sono presenti in datacite ma non in OpenAIRE? I campi con questi valori potrebbero dare problemi? Chiedere a OpenAIRE.

| Stato     | relationType          | Etichetta EN                             | Etichetta IT                                      |
|-----------|-----------------------|------------------------------------------|---------------------------------------------------|
| Nuovo     | IsObsoletedBy         | This upload is obsoleted by              | Questo contributo è reso obsoleto da              |
| Nuovo     | Obsoletes             | This upload obsoletes                    | Questo contributo rende obsoleto                  |
| Nuovo     | IsCollectedBy         | This upload is collected by              | Questo contributo è raccolto attraverso           |
| Nuovo     | Collects              | This upload collects                     | Questo contributo raccoglie                       |
| Nuovo     | IsTranslationOf       | This upload is a translation of          | Questo contributo è una traduzione di             |
| Nuovo     | HasTranslation        | This upload has a translation            | Questo contributo è tradotto in                   |

Esempio di mappatura dei ```relatedId``` e dei singoli file.

Mappare i singoli file con ```relationType="HasPart"``` le nuove o le precedenti versioni con ```relationType="IsNewVersionOf"``` o ```"IsPreviousVersionOf"```.

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

=== "OpenAIRE xml"

    ```xml
    <datacite:relatedIdentifiers>
        <datacite:relatedIdentifier relatedIdentifierType="DOI" relationType="IsNewVersionOf">10.6092/unibo/amsacta/8307</datacite:relatedIdentifier>
        <datacite:relatedIdentifier relatedIdentifierType="DOI" relationType="IsSupplementTo">10.1080/17452759.2025.2526032</datacite:relatedIdentifier>
        <datacite:relatedIdentifier relatedIdentifierType="URL" relationType="HasPart">https://amsacta.unibo.it/id/document/24241010</datacite:relatedIdentifier>
    </datacite:relatedIdentifiers>       
    ```

Per i capitoli di libro, aggiungere ISBN del volume con ```relationType="IsPublishedIn"```.

=== "AMS Acta json"

    ```json
    "type": "book_section",
    "isbn": {
        "$numberLong": "9788854971844"
    },
    "issn": "2035-553X"
    ```
=== "OpenAIRE xml"

    ```xml
    <datacite:relatedIdentifiers>
        <datacite:relatedIdentifier relatedIdentifierType="ISBN" relationType="IsPublishedIn">9788854971844</datacite:relatedIdentifier>
    </datacite:relatedIdentifiers>
    ```

Per i libri in collana, aggiungere ISSN della collana con ```relationType="IsPartOf"```

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "issn": "2724-2583"
    }
    ```

=== "OpenAire 4.0.1 xml"

    ```xml
    <datacite:relatedIdentifiers>
        <datacite:relatedIdentifier relatedIdentifierType="ISSN" relationType="IsPartOf">2724-2583</datacite:relatedIdentifier>
    </datacite:relatedIdentifiers>
    ```

# 7. Embargo Period date (MA)

Come per [DataCite](proprieta-datacite.md#8-date), per ogni file, se esiste una data di embargo (```documents.date_embargo``` o ```documents.date_embargo_retained```), la data di embargo viene mappata sul campo ```dates``` con l'attributo ```dateType="Available"```. <!--- la proprietà [Access Rights](#15-access-rights-m) deve essere "embargoed access".--->

=== "AMS Acta json"

    ```json
    {
        "datestamp": "2025-05-23 14:10:15",
        "documents": [
        {            
            "date_embargo_retained": "2025-06-30",
        }
    ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <datacite:dates>
    <datacite:date dateType="Accepted">2025-05-23T14:10:15Z</datacite:date>
    <datacite:date dateType="Available">2025-06-30</datacite:date>
    </datacite:dates>
    ```

Le date, seguendo le indicazioni riportate [qui](https://www.w3.org/TR/NOTE-datetime) possono essere esposte nei seguenti formati:

```
YYYY
YYYY-MM
YYYY-MM-DD
YYYY-MM-DDTHH:MM:SSZ (i datestamp di AMS Acta sono già espressi in UTC)
```

# 8. Language (MA)

Al contrario di [DataCite](proprieta-datacite.md#9-language), il campo è moltiplicabile. Utilizziamo la rappresentazione ISO 639-1, perché è quella già in uso in AMS Acta.

=== "AMS Acta json" 

    ```json
    { 
        "documents": [
            {
            "pos": 1,
            "language": "it"
            }
            {
            "pos": 2,
            "language": "en"
            }
        ]
    }
    ```
=== "OpenAIRE xml"

    ```xml
    <dc:language>it</dc:language>
    <dc:language>en</dc:language>
    ```

# 9. Publisher (MA)

Valutare in futuro se aggiungere il ROR dell'editore.

=== "AMS Acta json" 

    ```json
    {
        "publisher": "University of Bologna"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <dc:publisher>University of Bologna</dc:publisher>
    ```

# 10. Publication Date (M)

Usiamo il campo ```date```.

=== "AMS Acta json" 

    ```json
    {
        "date": "2025-05-01",
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <datacite:date dateType="Issued">2025-05-01</datacite:date>
    ```

# 11. Resource Type (M)

Vedere la [sezione specifica](resource-types.md).

# 12. Description (MA)

Mappare il campo ```abstract```. Il campo della lingua viene preso dalla lingua del primo file allegato.

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

=== "OpenAIRE"

    ```xml
    <dc:description xml:lang="it">Vengono trattati i fondamenti generali di energetica e i principi di funzionamento e gli schemi di realizzazione degli impianti non convenzionali, (nucleari a fissione e a fusione), e da fonti rinnovabili, (solare, idraulico, eolico, biomasse, geotermico), per la produzione di energia e i sistemi avanzati di conversione energetica, (celle a combustibile, fotovoltaica, magnetofluidodinamica, termoelettrica diretta, termoelettronica).\r\nVengono forniti i criteri generali di analisi degli investimenti e dei profitti per l'ottimizzazione dei sistemi impiantistici e i criteri di economia energetica degli impianti di produzione e conversione energetica.\r\nSi esaminano i criteri tecnici ed economici degli interventi per il risparmio e il recupero energetico e l'impiego di rifiuti e inquinanti per la produzione di combustibili pregiati.</dc:description>
    ```

# 13. Format (R)

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
        ]
    }
    ]
    ```

=== "OpenAIRE xml"
    ```xml
    <dc:format>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</dc:format>
    <dc:format>application/zip</dc:format>
    ```

# 14. Resource Identifier (M)

Utilizziamo il campo ```doi```.

=== "AMS Acta json" 

    ```json
    {
        "doi": "10.13123/unibo/amsactatest/7009"
    }
    ```

=== "DataCite xml"

    ```xml
    <datacite:identifier identifierType="DOI">10.13123/unibo/amsactatest/7009</datacite:identifier>
    ```

# 15. Access Rights (M)

Il campo non è moltiplicabile e deve descrivere la risorsa principale.

Laddove esista almeno un documento che presenti i metadati ```document.date_embargo``` o ```document.date_embargo_retained```, allora il valore deve essere ```embargoed access```.

=== "AMS Acta json" 

    ```json
    "documents": [
        {
            "date_embargo": "2026-04-01",
            "date_embargo_retained": "2026-04-01",
        }
    ]
    ```

=== "OpenAIRE xml"

    ```xml
    <datacite:rights rightsURI="http://purl.org/coar/access_right/c_f1cf">embargoed access</datacite:rights>
    ```

Se il file più pesante è chiuso (```"security": "staffonly",```), allora esponiamo il record come ```restricted access```.

=== "AMS Acta json"

    ```json
    "documents": [
    {
        "security": "staffonly",
        "files": [
        {
            "filesize": 4548526,
        }
        ],
    }
    {
        "security": "public",
        "files": [
        {
            "filesize": 1985,
        }
        ]
    }
    ]
    ```

=== "OpenAIRE xml"

    ```xml
    <datacite:rights rightsURI="http://purl.org/coar/access_right/c_16ec">restricted access</datacite:rights>
    ```


<!--Al momento, se almeno un file è aperto consideriamo il record aperto. Ad esempio, per il record [8128](https://amsacta.unibo.it/8128).

```xml
    <dc:rights>info:eu-repo/semantics/openAccess</dc:rights>
```

Forse dovremmo fare il contrario. Se almeno un file è ad accesso riservato, e se non esistono ```document.date_embargo``` o ```document.date_embargo_retained```, allora tutto il record deve risultare ad accesso riservato.

=== "AMS Acta json"
    
    ```json
    {
        "documents": [
            {
                "security": "staffonly"
            }
            {
                "security": "public"
            }
        ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
         <datacite:rights rightsURI="http://purl.org/coar/access_right/c_16ec">restricted access</datacite:rights>
    ```
-->
Se abbiamo il valore ```"full_text_status": "none"``` allora il documento è in modalità ```medatadata only access```.

=== "AMS Acta json"
    
    ```json
    {
        "full_text_status: "none"
    }
    ```

=== "OpenAIRE xml"

    ```xml
         <datacite:rights rightsURI="http://purl.org/coar/access_right/c_14cb">metadata only access</datacite:rights>
    ```

Altrimenti, la risorsa è in accesso aperto

=== "AMS Acta json"
    
    ```json
    {
        "documents": [
            {
                "security": "public"
            }
        ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
         <datacite:rights rightsURI="http://purl.org/coar/access_right/c_abf2">open access</datacite:rights>
    ```

# 16. Source (R)

Non esposto.

# 17. Subject (MA)

Come da [linee guida](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/4.0.1/field_subject.html), esporre le keywords separate da punti e virgola (;), o ripetere i campi con una keyword per volta.

I settori scientifico-disciplinari e gli ERC panel dovrebbero fare riferimento ad un vocabolario controllato (vedi esempio ottimale).

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

=== "OpenAIRE xml"

    ```xml
    <datacite:subjects>
        <datacite:subject xml:lang="en">urban spaces</datacite:subject>
        <datacite:subject xml:lang="en">metropolis</datacite:subject>
        <datacite:subject xml:lang="en">cities</datacite:subject>
        <datacite:subject xml:lang="en">digital technologies</datacite:subject>
        <datacite:subject xml:lang="en">automation</datacite:subject>
        <datacite:subject xml:lang="en">AI</datacite:subject>
        <datacite:subject xml:lang="en">smart city</datacite:subject>
        <datacite:subject xml:lang="it">M-GGR-01 Geografia</datacite:subject>
        <datacite:subject xml:lang="it">SPS-10 Sociologia dell'ambiente e del territorio</datacite:subject>
        <datacite:subject xml:lang="en">SH2-11 Human, economic and social geography</datacite:subject>
    </datacite:subjects>
    ```

=== "OpenAIRE xml (ottimale)"

    ```xml
    <datacite:subjects>
        <datacite:subject xml:lang="en">urban spaces</datacite:subject>
        <datacite:subject xml:lang="en">metropolis</datacite:subject>
        <datacite:subject xml:lang="en">cities</datacite:subject>
        <datacite:subject xml:lang="en">digital technologies</datacite:subject>
        <datacite:subject xml:lang="en">automation</datacite:subject>
        <datacite:subject xml:lang="en">AI</datacite:subject>
        <datacite:subject xml:lang="en">smart city</datacite:subject>
        <datacite:subject xml:lang="it" subjectScheme="Classificazione degli ambiti disciplinari" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines/019-011">M-GGR-01 Geografia</datacite:subject>
        <datacite:subject xml:lang="it" subjectScheme="Classificazione degli ambiti disciplinari" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines/025-010">SPS-10 Sociologia dell'ambiente e del territorio</datacite:subject>
        <datacite:subject xml:lang="en" subjectScheme="Vocabolario Controllato 2019 ERC EVALUATION PANEL e KEYWORD" schemeURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-her/erc-panel-h2020-fp" valueURI="https://w3id.org/italia/controlled-vocabulary/classifications-for-her/erc-panel-h2020-fp/SH2-11">SH2-11 Human, economic and social geography</datacite:subject>
    </datacite:subjects>
    ```

# 18. License Condition (R)

Deve essere un valore unico. Scegliamo la licenza del file più pesante. Come ```startDate``` utilizziamo, in ordine ```documents.date_embargo```, ```documents.date_embargo_retained```, oppure ```datestamp```.

=== "AMS Acta json"

    ```json
    {
        "datestamp": "2025-05-23 14:10:15",
        "documents": [
            {
            "language": "en",
            "license": "cc_by_4",
            "pos": 1, 
            "date_embargo_retained": "2025-06-30"
            }
            {
            "language": "it",
            "license": "studio_ricerca",
            "pos": 2
            }    
        ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:licenseCondition startDate="" uri="https://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International</oaire:licenseCondition>
    ```

Questo sistema genera incongruenze, ad esempio nel caso di [8128](https://amsacta.unibo.it/8128), che risulterebbe ad accesso riservato ma con licenza CC0.

# 19. Coverage (r)

Non lo esponiamo.

# 20. Size (O)

Per ogni allegato, specificare la dimensione in byte.

=== "AMS Acta json" 

    ```json
        "pages": 78
        "documents": [
        {
            "files": [
            {
                "filesize": 34649250
            }
            ],
        }    
        ]
    ```
    
=== "OpenAIRE xml"

    ```xml
    <datacite:sizes>
        <datacite:size>34649250</datacite:size>
        <datacite:size>78 pages</datacite:size>
    </datacite:sizes>
    ```

# 21. Geo Location (O)

Per ora esponiamo solo la sottoproprietà ```datacite:geoLocationPlace``` (testo libero).

=== "AMS Acta json"

    ```json
    "geolocplace": [
        {
        "place": "Bologna, Italy"
        }
    ],
    ```

=== "OpenAIRE xml"

    ```xml
    <datacite:geoLocations>
        <datacite:geoLocation>
            <datacite:geoLocationPlace>Bologna, Italy</datacite:geoLocationPlace>
        </datacite:geoLocation>
    </datacite:geoLocations>
    ```

# 22. Resource Version (R)

Decidere se esporre seguendo le indicazioni [qui](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/4.0.1/field_resourceversion.html).

Se vogliamo introdurre il sistema di open peer review occorre creare un nuovo metadato ed esporlo in questo campo.

# 23. File Location (MA)

Per ogni file bisogna esporre la URI (```documents.files.uri```), il mimetype (```documents.files.mime_type```), la tipologia del file e l'accessibilità.

Per l'attributo ```accessRightsUri```, usare i seguenti valori.

|                conceptURI                |         label        |
|------------------------------------------|----------------------|
| http://purl.org/coar/access_right/c_abf2 | open access          |
| http://purl.org/coar/access_right/c_f1cf | embargoed access     |
| http://purl.org/coar/access_right/c_16ec | restricted access    |
| http://purl.org/coar/access_right/c_14cb | metadata only access |

Se abbiamo ```document.security: "staffonly"``` e ```document.date_embargo``` o ```date_embargo_retained```esistono, allora scegliamo ```embargoed access```.

Se abbiamo ```document.security: "staffonly"``` allora scegliamo ```restricted access```.

Altrimenti, scegliamo ```open access```.

Per l'attributo ```objectType``` scegliamo

- ```dataset``` per ```type: dataset``` (anche per i readme file)
- ```software``` per ```type: software``` (anche per i readme file)
- ```fulltext``` tutte le altre tipologie.

<!--
EPrints aggiunge automaticamente alcuni documenti (preview e thumbnails) quando si aggiungono file PDF (o immagine?). Questi file si riconoscono attraverso il campo ```documents.formatdesc``` e ```documents.main```. Escludiamo questi file dalla mappatura. Ecco i casi che ho trovato (potrebbero essercene di più).

```
"formatdesc": "Thumbnails conversion from text to thumbnail_lightbox"
"formatdesc": "Thumbnails conversion from text to thumbnail_preview"
"formatdesc": "Thumbnails conversion from text to thumbnail_small"
"formatdesc": "Thumbnails conversion from text to thumbnail_medium"
```

Il nome di questi file è rispettivamente

```
"main": "lightbox.jpg"
"main": "preview.jpg"
"main": "small.jpg"
"main": "medium.jpg"
```
-->

Esempio ```embargoed_access```

=== "AMS Acta json"

    ```json
    {
    "type": "dataset",
    "documents": [
        {
            "date_embargo": "2026-04-01",
            "uri": "https://amsacta.unibo.it/id/document/23220319",
            "files": [
                {
                    "mime_type": "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"
                    "uri": "https://amsacta.unibo.it/id/file/23309047",
                }
            ]
        }
    ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
        <oaire:file accessRightsURI="http://purl.org/coar/access_right/c_f1cf" mimeType="application/vnd.openxmlformats-officedocument.spreadsheetml.sheet" objectType="dataset">https://amsacta.unibo.it/id/document/23220319</oaire:file>
    ```

Esempio ```restricted access``` e ```open_access```

=== "AMS Acta json"

    ```json
    {
        "eprintid": 7552,
        "documents": [
            {
                "security": "staffonly",
                "language": "en",
                "mime_type": "application/zip",
                "uri": "https://amsacta.unibo.it/id/document/15570485",
                "files": [
                    {
                        "mime_type": "application/zip",
                        "uri": "https://amsacta.unibo.it/id/file/15643966",
                    }
                ],
            },
            {
                "uri": "https://amsacta.unibo.it/id/document/15570486",
                "security": "public",
                "mime_type": "application/vnd.oasis.opendocument.text",
                "files": [
                    {
                    "filename": "Una.Resin_WP2_T2.2_benchmarking-questionnaire_template_20231103.odt",
                    "mime_type": "application/vnd.oasis.opendocument.text",
                    "uri": "https://amsacta.unibo.it/id/file/15643970"
                    }
                ]
            }
        ]
    }
    ```

=== "OpenAIRE xml"

    ```xml
        <oaire:file accessRightsURI="http://purl.org/coar/access_right/c_16ec" mimeType="application/zip" objectType="dataset">https://amsacta.unibo.it/id/document/15570485</oaire:file>
        <oaire:file accessRightsURI="http://purl.org/coar/access_right/c_abf2" mimeType="application/zip" objectType="dataset">https://amsacta.unibo.it/id/document/15570486</oaire:file>
    ```

# 24. Citation Title (R)

## Estratti da libro

=== "AMS Acta json"

    ```json
    {
        "type": "book_section",
        "book_title": "Vol. 18/2025",
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationTitle>Vol. 18/2025</oaire:citationTitle>
    ```

## Documento relativo a evento

Titolo dell'evento

=== "AMS Acta json"

    ```json
    {
        "type": "conference_item",
        "event_title": "Simposio 2G-C",
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationTitle>Simposio 2G-C</oaire:citationTitle>
    ```
   
## Articoli

Titolo della rivista

=== "AMS Acta json"

    ```json
    {
        "type": "article",
        "publication": "Psicologia di comunità"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationTitle>Psicologia di comunità</oaire:citationTitle>
    ```


## Monografie

Titolo della collana? (Aperta issue)

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "series": "I Quaderni di Into the Black Box",

    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationTitle>I Quaderni di Into the Black Box</oaire:citationTitle>
    ```

# 25. Citation Volume (R)

## Estratti da libro

=== "AMS Acta json"

    ```json
    {
        "type": "book_section",
        "volume": 18,
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationVolume>18</oaire:citationVolume>
    ```

## Articoli

Numero del volume della rivista

=== "AMS Acta json"

    ```json
    {
        "type": "article",
        "volume": 10,
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationVolume>77</oaire:citationVolume>
    ```

## Monografie

Numero del volume nella collana?

=== "AMS Acta json"

    ```json
    {
        "type": "article",
        "volume": 10,
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationVolume>77</oaire:citationVolume>
    ```

26. Citation Issue (R)

## Articoli

Numero del fascicolo della rivista.

=== "AMS Acta json"

    ```json
    {
        "type": "article",
        "number": 10,
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationIssue>10</oaire:citationIssue>
    ```

27. Citation Start Page (R)

=== "AMS Acta json"

    ```json
    {
        "pagerange": "1-15"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationStartPage>1</oaire:citationStartPage>
    ```

28. Citation End Page (R)

=== "AMS Acta json"

    ```json
    {
        "pagerange": "1-15"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationEndPage>15</oaire:citationEndPage>
    ```

29. Citation Edition (R)

Non ce lo abbiamo.

30. Citation Conference Place (R)

=== "AMS Acta json"

    ```json
    {
        "event_location": "Bologna, Italy"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationConferencePlace>Bologna, Italy</oaire:citationConferencePlace>
    ```

31. Citation Conference Date (R)

=== "AMS Acta json"

    ```json
    {
        "event_dates": "2-6 october 2000"
    }
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:citationConferenceDate>2-6 october 2000</oaire:citationConferenceDate>
    ```

32. Audience (O)

Non ce lo abbiamo