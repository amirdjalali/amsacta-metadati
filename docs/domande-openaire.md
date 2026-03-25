# Related identifier

Some ```relationType``` are present in DataCite 4.6 but not in OpenAIRE 4.0. OpenAIRE 4.0.1 adds only ```IsPublishedIn```. The following are still missing

```
IsObsoletedBy 	
Obsoletes 	
IsCollectedBy 	
Collects 	
IsTranslationOf 	
HasTranslation
```

# Access Rights and License Condition

What do we do if our dataset has more documents with different access conditiond and licenses? For instance, record [8128](https://amsacta.unibo.it/8128). Shall we consider the first file? Or shall we consider the record closed since at least one document (the main document) is closed?

# Add properties

Proposed properties

```
citationSeries
citationSeriesCurators
citationVolumeEditors
```