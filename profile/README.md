# Ulysses

Ulysses project contains machine learning modules designed to the Brazil's Chamber of Deputies.

---

```mermaid
flowchart LR

optimizer("Ulysses Optimizer")
curiosity("Ulysses Curiosity")
segmenter("Ulysses Segmenter")
fetcher("Ulysses Fetcher")

subgraph comparer["Ulysses Document Comparer"]
    direction TB
    expandQuery["expand-query"]
    lookForReferenced["look-for-referenced"]
    lookForSimilar["look-for-similar"]
    saveRelevanceFeedback["save-relevance-feedback"]

    expandQuery --- lookForReferenced --- lookForSimilar --- saveRelevanceFeedback

    linkStyle 0 stroke-width:0px;
    linkStyle 1 stroke-width:0px;
    linkStyle 2 stroke-width:0px;
end

subgraph analyzer["Ulysses Argumentation Analyzer"]
    direction TB
    clusterComments
    mapToDocument

    clusterComments --- mapToDocument

    linkStyle 3 stroke-width:0px;
end

segmenter --> analyzer
fetcher   --> analyzer
fetcher   --> segmenter
optimizer --> analyzer

analyzer --- comparer
linkStyle 8 stroke-width:0px;

classDef default fill:#333333,color:white,stroke-width:2px,stroke:#AAAAAA;
classDef clsBaseModule fill:#4D644D;
classDef clsIntegrationModule fill:#644D51,font-size:13px;
classDef clsMicroservice fill:#514D64,font-size:16px;

class optimizer,curiosity,segmenter,fetcher clsBaseModule;
class analyzer,comparer clsIntegrationModule;
class clusterComments,mapToDocument,expandQuery,lookForReferenced,lookForSimilar,saveRelevanceFeedback clsMicroservice;
```

---

## Available modules
1. Base modules:
    - *Ulysses Fetcher:* fetch pretrained models stored in cloud services;
    - *Ulysses Optimizer:* quantization and optimization methods pretrained model;
    - *Ulysses Segmenter:* semantic segmentation of legal documents into legal items;
    - *Ulysses Curiosity:* probe and validate pretrained models;
2. Integration modules:
    - *Ulysses Argumentation Analyzer:*
        - (microservice) clusterComments;
        - (microservice) mapToDocument.
    - *Ulysses Document Comparer:*
        - (microservice) look-for-similar;
        - (microservice) look-for-referenced;
        - (microservice) expand-query;
        - (microservice) save-relevance-feedback.

## Publication code
Additional research code meant for scientific publication is available at [Ulysses (publicações)](https://github.com/Convenio-Camara-dos-Deputados).
