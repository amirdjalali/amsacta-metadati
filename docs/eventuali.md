# Eventuali aggiornamenti per il futuro

## Permettere che un autore sia anche una istituzione.

*** FATTO ***

Se l'autore può essere una istituzione, allora dobbiamo aggiungere l'attributo nameType (valori ammessi Personal e Organizational) al tag reatorName per indicare che si tratta di una persona o una istituzione.

```xml
<creator>
    <creatorName nameType="Personal">minnie, topolina</creatorName>
    <givenName>topolina</givenName>
    <familyName>minnie</familyName>
    <affiliation>University of Bologna, Dipartimento delle Arti</affiliation>
    <nameIdentifier schemeURI="http://orcid.org/" nameIdentifierScheme="ORCID">0000-0002-9494-5384</nameIdentifier>
</creator>
```

## Duplicare il titolo in più lingue

Se serve, possiamo valutare la possibilità di duplicare il titolo, per inserirlo in lingue diverse.

## Aggiornare gli schemi degli SSD e degli ERC panels

Gli schemi attuali sono qui:

- SSD: https://w3id.org/italia/controlled-vocabulary/classifications-for-culture/subject-disciplines
- ERC panels: https://w3id.org/italia/controlled-vocabulary/classifications

Una issue per l'aggiornamento degli schemi è stata aperta su GitHub [qui](https://github.com/italia/dati-semantic-assets/issues/298).