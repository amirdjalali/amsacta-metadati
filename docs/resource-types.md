Il vocabolario controllato di DataCite dei valori ammessi per ```resourceTypeGeneral``` è disponibile [qui](https://datacite-metadata-schema.readthedocs.io/en/4.6/properties/resourcetype/).

Privilegiare sempre la scelta di un valore per ```resourceTypeGeneral``` tra quelli presenti nel vocabolario controllato, in assenza di un valore specifico, si è scelto di utilizzare il valore generico ```Text```.

[OpenAIRE](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/stable/field_publicationtype.html#) invece utilizza il vocabolario controllato di COAR.

# Dataset

=== "AMS Acta json"

    ```json
    {
        "type": "dataset"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Dataset"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="dataset" uri="http://purl.org/coar/resource_type/c_ddb1">dataset</oaire:resourceType>
    ```

# Documento relativo ad un convegno o altro evento

## Atto

=== "AMS Acta json"

    ```json
    {
        "type": "conference_item",
        "pres_type": "paper"
    }
    ```

=== "DataCite xml"

    ```xml
    <resourceType resourceTypeGeneral="ConferenceProceeding"/>
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_5794">conference paper</oaire:resourceType>
    ```

## Presentazione, Altro

=== "AMS Acta json"

    ```json
    {
        "type": "conference_item",
        "pres_type": "slide"    // oppure "other"
    }
    ```

=== "DataCite xml"

    ```xml
    <resourceType resourceTypeGeneral="Text">Conference Output</resourceType>
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_c94f">conference object</oaire:resourceType>
    ```

## Poster

=== "AMS Acta json"

    ```json
    {
        "type": "conference_item",
        "pres_type": "poster"
    }
    ```

=== "DataCite xml"

    ```xml
    <resourceType resourceTypeGeneral="Text">Conference Output</resourceType>
    ```

=== "OpenAIRE xml"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_6670">conference poster</oaire:resourceType>
    ```

# Estratto da libro

=== "AMS Acta json"

    ```json
    {
        "type": "book_section"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book Chapter"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_3248">book part</oaire:resourceType>
    ```

Per questa tipologia bisogna anche esporre il libro da cui è tratto l'estratto, popolando le proprietà ```relatedIdentifier``` e ```relatedItem```. Per dettagli vedi [qui](proprieta-datacite.md#12-relatedidentifiers) e [qui](proprieta-datacite.md#20-relateditem).

# Monografia

Per tutte queste sotto-tipologie, se è associato un ISBN al volume, o è specificato un ISSN della collana a cui il volume appartiene, occorre anche esporle popolando le proprietà ```relatedIdentifier``` e ```relatedItem```. Per dettagli vedi [qui](proprieta-datacite.md#12-relatedidentifiers) e [qui](proprieta-datacite.md#20-relateditem).

## Libro

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "libro"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```


## Atti di convegno

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "atti_convegno"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="ConferenceProceeding"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_f744">conference proceedings</oaire:resourceType>
    ```

## Trattato

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "trattato"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Treatise</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```


## Edizione critica

In DataCite e in OpenAIRE non è prevista. Potremmo fare così per ora

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "edizione_critica"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Critical edition</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```


## Rapporto tecnico

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "technical_report"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Report">Technical Report</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_18gh">technical report</oaire:resourceType>
    ```

## Manuale

Quale voce utilizzare per [OpenAIRE](https://openaire-guidelines-for-literature-repository-managers.readthedocs.io/en/latest/field_publicationtype.html)?

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "manual"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Manual</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_71bd">technical documentation</oaire:resourceType>
    ```

## Antologia

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "manual"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Anthology</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

## Working paper

Questa tipologia è specifica per le monografie all’interno di collane. Suggerirei quindi di usare la tipologia "Book"

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "working_paper"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Working paper</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

## Catalogo

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "catalogo"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Catalog</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

## Traduzione

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "traduzione"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Translation</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

## Saggio

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "saggio"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Essay</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

## Altro

=== "AMS Acta json"

    ```json
    {
        "type": "monograph",
        "monograph_type": "other"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Book">Other</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_2f33">book</oaire:resourceType>
    ```

# Preprint

=== "AMS Acta json"

    ```json
    {
        "type": "preprint"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Preprint"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_816b">preprint</oaire:resourceType>
    ```

# Working Paper

Non c’è una categoria specifica per il working paper in DataCite, ma c'è in OpenAIRE

=== "AMS Acta json"

    ```json
    {
        "type": "working_paper"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Text">Working paper</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_8042">working paper</oaire:resourceType>
    ```

# Software

=== "AMS Acta json"

    ```json
    {
        "type": "software"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Software"/>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="software" uri="http://purl.org/coar/resource_type/c_5ce6">software</oaire:resourceType>
    ```

# Articolo

Possiamo scegliere tra ```[journal article](http://purl.org/coar/resource_type/c_6501)``` e ```[research article](http://purl.org/coar/resource_type/c_2df8fbb1)```

=== "AMS Acta json"

    ```json
    {
        "type": "article"
    }
    ```

=== "DataCite"

    ```xml
    <resourceType resourceTypeGeneral="Text">Article</resourceType>
    ```

=== "OpenAIRE"

    ```xml
    <oaire:resourceType resourceTypeGeneral="literature" uri="http://purl.org/coar/resource_type/c_6501">journal article</oaire:resourceType>
    ```

# Tesi

Non sono presenti in archivio.
