# Ulysses

Ulysses project contains machine learning modules designed to the Brazil's Chamber of Deputies.

---

```mermaid
flowchart LR

package_optimizer("Ulysses Optimizer")
package_curiosity("Ulysses Curiosity")
package_segmenter("Ulysses Segmenter")
package_fetcher("Ulysses Fetcher")

subgraph microservice_comparer["Ulysses Document Comparer"]
    direction TB
    microservice_expandQuery["expand-query"]
    microservice_lookForReferenced["look-for-referenced"]
    microservice_lookForSimilar["look-for-similar"]
    microservice_saveRelevanceFeedback["save-relevance-feedback"]

    microservice_expandQuery --- microservice_lookForReferenced --- microservice_lookForSimilar --- microservice_saveRelevanceFeedback

    linkStyle 0 stroke-width:0px;
    linkStyle 1 stroke-width:0px;
    linkStyle 2 stroke-width:0px;
end

subgraph microservice_analyzer["Ulysses Argumentation Analyzer"]
    direction TB
    microservice_clusterComments["clusterComments"]
    microservice_mapToDocument["mapToDocument (map2doc)"]

    microservice_clusterComments --- microservice_mapToDocument

    linkStyle 3 stroke-width:0px;
end

package_segmenter --> microservice_analyzer
package_fetcher   --> microservice_analyzer
package_optimizer --> microservice_analyzer
package_fetcher   --> package_segmenter
package_fetcher   --> package_curiosity

microservice_analyzer --- microservice_comparer
linkStyle 9 stroke-width:0px;

classDef default fill:#333333,color:white,stroke-width:2px,stroke:#AAAAAA;
classDef clsBaseModule fill:#4D644D;
classDef clsIntegrationModule fill:#644D51,font-size:13px,color:white;
classDef clsMicroservice fill:#514D64,font-size:16px;

class package_optimizer,package_curiosity,package_segmenter,package_fetcher clsBaseModule;
class microservice_analyzer,microservice_comparer clsIntegrationModule;
class microservice_clusterComments,microservice_mapToDocument clsMicroservice;
class microservice_expandQuery,microservice_lookForReferenced,microservice_lookForSimilar,microservice_saveRelevanceFeedback clsMicroservice;
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
