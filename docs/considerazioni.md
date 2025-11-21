# Considerazioni generali

I metadati devono essere registrati nei metadati di DataCite al momento della creazione del DOI, ed esposti nell'interfaccia OAI-PMH.

In tutti i tag XML, rimuovere lo spazio prima del simbolo di chiusura ```>```.

Per indicare la lingua principale del contributo è stata utilizzata la lingua del primo file caricato.

```json
"documents": [
            {
                "language": "en",
                "pos": 1
            },
]
```

Questo campo verrà usato per il metadato Language e per l'attributo ```xml:lang``` dei campi [Title](proprieta-datacite.md#3-title), [Subject](proprieta-datacite.md#6-subject), [Description](proprieta-datacite.md#17-descriptions) e [Rights](proprieta-datacite.md#16-rights).