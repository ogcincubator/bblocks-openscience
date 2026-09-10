
# Geospatial Processing Step Provenance (Schema)

`ogc.osc.prov-processing-step` *v0.1.0*

A profile of the PROV-O building block constrained to the description of a single geospatial processing step, with a required link to a registered process type.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Geospatial Processing Step Provenance

This building block profiles `ogc-utils.prov` down to a single unit: one
geospatial processing step.

PROV-O is deliberately general. Any valid PROV document is a valid description
of a processing step, which makes validation weak and cross-platform comparison
hard.

OGC API - Processes Part 5 (draft 26-038) narrows this for job provenance: a
job entity, a process entity, an activity joining them, and input/output
artifacts carrying roles. This profile follows that shape.

Part 5 does not define any link from a process to a registered process type.
This profile makes that link required, via the processType property. It is the
point at which the OSPD 2026 profile-plus-register pattern closes: the profile
gives the structure, the register gives the controlled term.

Under development as part of OSPD 2026, deliverable D104 (Aganitha Space
Technologies, Workflow Profiler).

## Examples

### Ingest of mandal-level vegetation and soil moisture
#### json
```json
{
  "id": "urn:aganitha:step:ingest-dicra:20260807T060000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/ingest",
  "label": "Ingest mandal NDVI and soil moisture",
  "startedAtTime": "2026-08-07T06:00:00Z",
  "endedAtTime": "2026-08-07T06:03:41Z",
  "used": ["urn:aganitha:source:dicra-mandal-archive"],
  "generated": ["urn:aganitha:dataset:mandal-ndvi-sm-merged"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:source:dicra-mandal-archive",
      "hadRole": "https://example.org/ospd/roles/sourceArchive"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:ingest-dicra:20260807T060000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/ingest",
  "label": "Ingest mandal NDVI and soil moisture",
  "startedAtTime": "2026-08-07T06:00:00Z",
  "endedAtTime": "2026-08-07T06:03:41Z",
  "used": [
    "urn:aganitha:source:dicra-mandal-archive"
  ],
  "generated": [
    "urn:aganitha:dataset:mandal-ndvi-sm-merged"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:source:dicra-mandal-archive",
      "hadRole": "https://example.org/ospd/roles/sourceArchive"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<urn:aganitha:step:ingest-dicra:20260807T060000Z> a prov:Activity ;
    rdfs:label "Ingest mandal NDVI and soil moisture" ;
    dct:type <https://example.org/ospd/process-types/ingest> ;
    prov:endedAtTime "2026-08-07T06:03:41+00:00"^^xsd:dateTime ;
    prov:generated <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:source:dicra-mandal-archive> ;
            prov:hadRole <https://example.org/ospd/roles/sourceArchive> ] ;
    prov:startedAtTime "2026-08-07T06:00:00+00:00"^^xsd:dateTime ;
    prov:used <urn:aganitha:source:dicra-mandal-archive> .


```


### Normalisation of vegetation index to a condition index
#### json
```json
{
  "id": "urn:aganitha:step:vci:20260807T061000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-normalisation",
  "label": "Compute vegetation condition index from NDVI",
  "used": [
    "urn:aganitha:dataset:mandal-ndvi-sm-merged",
    "urn:aganitha:reference:ndvi-extrema"
  ],
  "generated": ["urn:aganitha:dataset:vci"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:mandal-ndvi-sm-merged",
      "hadRole": "https://example.org/ospd/roles/observedIndex"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:reference:ndvi-extrema",
      "hadRole": "https://example.org/ospd/roles/normalisationReference"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:vci:20260807T061000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-normalisation",
  "label": "Compute vegetation condition index from NDVI",
  "used": [
    "urn:aganitha:dataset:mandal-ndvi-sm-merged",
    "urn:aganitha:reference:ndvi-extrema"
  ],
  "generated": [
    "urn:aganitha:dataset:vci"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:mandal-ndvi-sm-merged",
      "hadRole": "https://example.org/ospd/roles/observedIndex"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:reference:ndvi-extrema",
      "hadRole": "https://example.org/ospd/roles/normalisationReference"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:vci:20260807T061000Z> a prov:Activity ;
    rdfs:label "Compute vegetation condition index from NDVI" ;
    dct:type <https://example.org/ospd/process-types/index-normalisation> ;
    prov:generated <urn:aganitha:dataset:vci> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:reference:ndvi-extrema> ;
            prov:hadRole <https://example.org/ospd/roles/normalisationReference> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
            prov:hadRole <https://example.org/ospd/roles/observedIndex> ] ;
    prov:used <urn:aganitha:dataset:mandal-ndvi-sm-merged>,
        <urn:aganitha:reference:ndvi-extrema> .


```


### Normalisation of soil moisture to a deficit index
#### json
```json
{
  "id": "urn:aganitha:step:smdi:20260807T061500Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-normalisation",
  "label": "Compute soil moisture deficit index",
  "used": [
    "urn:aganitha:dataset:mandal-ndvi-sm-merged",
    "urn:aganitha:reference:soil-moisture-extrema"
  ],
  "generated": ["urn:aganitha:dataset:smdi"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:mandal-ndvi-sm-merged",
      "hadRole": "https://example.org/ospd/roles/observedIndex"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:reference:soil-moisture-extrema",
      "hadRole": "https://example.org/ospd/roles/normalisationReference"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:smdi:20260807T061500Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-normalisation",
  "label": "Compute soil moisture deficit index",
  "used": [
    "urn:aganitha:dataset:mandal-ndvi-sm-merged",
    "urn:aganitha:reference:soil-moisture-extrema"
  ],
  "generated": [
    "urn:aganitha:dataset:smdi"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:mandal-ndvi-sm-merged",
      "hadRole": "https://example.org/ospd/roles/observedIndex"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:reference:soil-moisture-extrema",
      "hadRole": "https://example.org/ospd/roles/normalisationReference"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:smdi:20260807T061500Z> a prov:Activity ;
    rdfs:label "Compute soil moisture deficit index" ;
    dct:type <https://example.org/ospd/process-types/index-normalisation> ;
    prov:generated <urn:aganitha:dataset:smdi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
            prov:hadRole <https://example.org/ospd/roles/observedIndex> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:reference:soil-moisture-extrema> ;
            prov:hadRole <https://example.org/ospd/roles/normalisationReference> ] ;
    prov:used <urn:aganitha:dataset:mandal-ndvi-sm-merged>,
        <urn:aganitha:reference:soil-moisture-extrema> .


```


### Weighted composition of a combined drought index
#### json
```json
{
  "id": "urn:aganitha:step:cdsi:20260807T062000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-composition",
  "label": "Compose combined drought severity index",
  "used": [
    "urn:aganitha:dataset:vci",
    "urn:aganitha:dataset:smdi"
  ],
  "generated": ["urn:aganitha:dataset:cdsi"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:vci",
      "hadRole": "https://example.org/ospd/roles/indexComponent"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:smdi",
      "hadRole": "https://example.org/ospd/roles/indexComponent"
    }
  ],
  "parameters": {
    "weights": { "vci": 0.6, "smdi": 0.4 }
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:cdsi:20260807T062000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/index-composition",
  "label": "Compose combined drought severity index",
  "used": [
    "urn:aganitha:dataset:vci",
    "urn:aganitha:dataset:smdi"
  ],
  "generated": [
    "urn:aganitha:dataset:cdsi"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:vci",
      "hadRole": "https://example.org/ospd/roles/indexComponent"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:smdi",
      "hadRole": "https://example.org/ospd/roles/indexComponent"
    }
  ],
  "parameters": {
    "weights": {
      "vci": 0.6,
      "smdi": 0.4
    }
  }
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:cdsi:20260807T062000Z> a prov:Activity ;
    rdfs:label "Compose combined drought severity index" ;
    dct:type <https://example.org/ospd/process-types/index-composition> ;
    prov:generated <urn:aganitha:dataset:cdsi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:vci> ;
            prov:hadRole <https://example.org/ospd/roles/indexComponent> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:smdi> ;
            prov:hadRole <https://example.org/ospd/roles/indexComponent> ] ;
    prov:used <urn:aganitha:dataset:smdi>,
        <urn:aganitha:dataset:vci> .


```


### Classification into drought severity classes
#### json
```json
{
  "id": "urn:aganitha:step:classify:20260807T063000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/classification",
  "label": "Classify drought severity",
  "used": [
    "urn:aganitha:dataset:cdsi",
    "urn:aganitha:scheme:drought-severity-classes"
  ],
  "generated": ["urn:aganitha:dataset:drought-classes"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/inputField"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:scheme:drought-severity-classes",
      "hadRole": "https://example.org/ospd/roles/classificationScheme"
    }
  ],
  "parameters": {
    "classBreaks": [0.30, 0.45, 0.60, 0.75]
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:classify:20260807T063000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/classification",
  "label": "Classify drought severity",
  "used": [
    "urn:aganitha:dataset:cdsi",
    "urn:aganitha:scheme:drought-severity-classes"
  ],
  "generated": [
    "urn:aganitha:dataset:drought-classes"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/inputField"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:scheme:drought-severity-classes",
      "hadRole": "https://example.org/ospd/roles/classificationScheme"
    }
  ],
  "parameters": {
    "classBreaks": [
      0.3,
      0.45,
      0.6,
      0.75
    ]
  }
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:classify:20260807T063000Z> a prov:Activity ;
    rdfs:label "Classify drought severity" ;
    dct:type <https://example.org/ospd/process-types/classification> ;
    prov:generated <urn:aganitha:dataset:drought-classes> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/inputField> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:scheme:drought-severity-classes> ;
            prov:hadRole <https://example.org/ospd/roles/classificationScheme> ] ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:scheme:drought-severity-classes> .


```


### Standardised precipitation index over an accumulation window
#### json
```json
{
  "id": "urn:aganitha:step:spi:20260807T064000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/standardised-index",
  "label": "Compute standardised precipitation index",
  "used": [
    "urn:aganitha:dataset:precipitation-series",
    "urn:aganitha:dataset:precipitation-reference-period"
  ],
  "generated": ["urn:aganitha:dataset:spi"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:precipitation-series",
      "hadRole": "https://example.org/ospd/roles/inputSeries"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:precipitation-reference-period",
      "hadRole": "https://example.org/ospd/roles/fittingReference"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:spi:20260807T064000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/standardised-index",
  "label": "Compute standardised precipitation index",
  "used": [
    "urn:aganitha:dataset:precipitation-series",
    "urn:aganitha:dataset:precipitation-reference-period"
  ],
  "generated": [
    "urn:aganitha:dataset:spi"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:precipitation-series",
      "hadRole": "https://example.org/ospd/roles/inputSeries"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:precipitation-reference-period",
      "hadRole": "https://example.org/ospd/roles/fittingReference"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:spi:20260807T064000Z> a prov:Activity ;
    rdfs:label "Compute standardised precipitation index" ;
    dct:type <https://example.org/ospd/process-types/standardised-index> ;
    prov:generated <urn:aganitha:dataset:spi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:precipitation-series> ;
            prov:hadRole <https://example.org/ospd/roles/inputSeries> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:precipitation-reference-period> ;
            prov:hadRole <https://example.org/ospd/roles/fittingReference> ] ;
    prov:used <urn:aganitha:dataset:precipitation-reference-period>,
        <urn:aganitha:dataset:precipitation-series> .


```


### Model training as a processing step
#### json
```json
{
  "id": "urn:aganitha:step:train:20260807T070000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/model-training",
  "label": "Train drought prediction model with spatial cross-validation",
  "used": [
    "urn:aganitha:dataset:cdsi",
    "urn:aganitha:dataset:spi",
    "urn:aganitha:dataset:drought-classes",
    "urn:aganitha:partition:district-folds"
  ],
  "generated": [
    "urn:aganitha:model:drought-classifier",
    "urn:aganitha:report:validation-metrics"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/trainingFeatures"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:spi",
      "hadRole": "https://example.org/ospd/roles/trainingFeatures"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:drought-classes",
      "hadRole": "https://example.org/ospd/roles/trainingTarget"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:partition:district-folds",
      "hadRole": "https://example.org/ospd/roles/validationPartition"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:train:20260807T070000Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/model-training",
  "label": "Train drought prediction model with spatial cross-validation",
  "used": [
    "urn:aganitha:dataset:cdsi",
    "urn:aganitha:dataset:spi",
    "urn:aganitha:dataset:drought-classes",
    "urn:aganitha:partition:district-folds"
  ],
  "generated": [
    "urn:aganitha:model:drought-classifier",
    "urn:aganitha:report:validation-metrics"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/trainingFeatures"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:spi",
      "hadRole": "https://example.org/ospd/roles/trainingFeatures"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:drought-classes",
      "hadRole": "https://example.org/ospd/roles/trainingTarget"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:partition:district-folds",
      "hadRole": "https://example.org/ospd/roles/validationPartition"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:train:20260807T070000Z> a prov:Activity ;
    rdfs:label "Train drought prediction model with spatial cross-validation" ;
    dct:type <https://example.org/ospd/process-types/model-training> ;
    prov:generated <urn:aganitha:model:drought-classifier>,
        <urn:aganitha:report:validation-metrics> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:partition:district-folds> ;
            prov:hadRole <https://example.org/ospd/roles/validationPartition> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/trainingFeatures> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:drought-classes> ;
            prov:hadRole <https://example.org/ospd/roles/trainingTarget> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:spi> ;
            prov:hadRole <https://example.org/ospd/roles/trainingFeatures> ] ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:dataset:drought-classes>,
        <urn:aganitha:dataset:spi>,
        <urn:aganitha:partition:district-folds> .


```


### Inference using a trained model
#### json
```json
{
  "id": "urn:aganitha:step:project:20260807T071500Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/model-inference",
  "label": "Generate forward drought projection",
  "used": [
    "urn:aganitha:model:drought-classifier",
    "urn:aganitha:dataset:cdsi"
  ],
  "generated": ["urn:aganitha:dataset:drought-projection"],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:model:drought-classifier",
      "hadRole": "https://example.org/ospd/roles/fittedModel"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/inferenceInput"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:aganitha:step:project:20260807T071500Z",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/model-inference",
  "label": "Generate forward drought projection",
  "used": [
    "urn:aganitha:model:drought-classifier",
    "urn:aganitha:dataset:cdsi"
  ],
  "generated": [
    "urn:aganitha:dataset:drought-projection"
  ],
  "qualifiedUsage": [
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:model:drought-classifier",
      "hadRole": "https://example.org/ospd/roles/fittedModel"
    },
    {
      "@type": "prov:Usage",
      "entity": "urn:aganitha:dataset:cdsi",
      "hadRole": "https://example.org/ospd/roles/inferenceInput"
    }
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:project:20260807T071500Z> a prov:Activity ;
    rdfs:label "Generate forward drought projection" ;
    dct:type <https://example.org/ospd/process-types/model-inference> ;
    prov:generated <urn:aganitha:dataset:drought-projection> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:model:drought-classifier> ;
            prov:hadRole <https://example.org/ospd/roles/fittedModel> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/inferenceInput> ] ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:model:drought-classifier> .


```


### Minimal conforming step
#### json
```json
{
  "id": "urn:example:step:0001",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/ingest",
  "used": ["urn:example:input:0001"],
  "generated": ["urn:example:output:0001"]
}

```

#### jsonld
```jsonld
{
  "@context": "https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld",
  "id": "urn:example:step:0001",
  "provType": "Activity",
  "processType": "https://example.org/ospd/process-types/ingest",
  "used": [
    "urn:example:input:0001"
  ],
  "generated": [
    "urn:example:output:0001"
  ]
}
```

#### ttl
```ttl
@prefix dct: <http://purl.org/dc/terms/> .
@prefix prov: <http://www.w3.org/ns/prov#> .

<urn:example:step:0001> a prov:Activity ;
    dct:type <https://example.org/ospd/process-types/ingest> ;
    prov:generated <urn:example:output:0001> ;
    prov:used <urn:example:input:0001> .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Geospatial Processing Step Provenance
description: A single geospatial processing step, expressed as a constrained profile
  of PROV-O. Inputs and outputs are entity references; the role each played is expressed
  through prov:qualifiedUsage rather than inline, so the profile stays compatible
  with the PROV-O object model.
allOf:
- $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov/schema.yaml
- type: object
  required:
  - id
  - processType
  - used
  - generated
  properties:
    id:
      description: Stable identifier for this processing step activity.
      type: string
    processType:
      description: Identifier of the registered process type this step is an instance
        of. This is the link that PROV-O and OGC API - Processes Part 5 do not themselves
        provide. Bound to dct:type rather than a newly minted term, so the value resolves
        as a governed concept in the process-type register.
      type: string
      x-jsonld-id: http://purl.org/dc/terms/type
      x-jsonld-type: '@id'
    label:
      type: string
      x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#label
    startedAtTime:
      type: string
      format: date-time
    endedAtTime:
      type: string
      format: date-time
    used:
      description: Entities consumed by this step.
      type: array
      minItems: 1
      items:
        type: string
    generated:
      description: Entities produced by this step.
      type: array
      minItems: 1
      items:
        type: string
    qualifiedUsage:
      description: Which declared input slot of the process type each consumed entity
        occupied. Makes two runs of the same process type comparable.
      type: array
      items:
        type: object
        required:
        - entity
        - hadRole
        properties:
          entity:
            type: string
          hadRole:
            type: string
    wasAssociatedWith:
      type: array
      items:
        type: string
    parameters:
      description: 'Parameter values that determined the behaviour of this step. Keys
        SHOULD be drawn from the parameter terms declared by the registered process
        type. Deliberately left unbound in the JSON-LD context: how parameters should
        be typed depends on whether process types are registered coarsely or as parameterised
        subtypes, which is still an open question for the register design.'
      type: object
      additionalProperties: true

```

Links to the schema:

* YAML version: [schema.yaml](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/schema.json)
* JSON version: [schema.json](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasInfluencedBy": {
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "featureType": "@type",
    "entityType": "@type",
    "has_provenance": {
      "@id": "dct:provenance",
      "@type": "@id"
    },
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
      "@type": "@id"
    },
    "wasAttributedTo": {
      "@id": "prov:wasAttributedTo",
      "@type": "@id"
    },
    "wasDerivedFrom": {
      "@id": "prov:wasDerivedFrom",
      "@type": "@id"
    },
    "alternateOf": {
      "@id": "prov:alternateOf",
      "@type": "@id"
    },
    "hadPrimarySource": {
      "@id": "prov:hadPrimarySource",
      "@type": "@id"
    },
    "specializationOf": {
      "@id": "prov:specializationOf",
      "@type": "@id"
    },
    "wasInvalidatedBy": {
      "@id": "prov:wasInvalidatedBy",
      "@type": "@id"
    },
    "wasQuotedFrom": {
      "@id": "prov:wasQuotedFrom",
      "@type": "@id"
    },
    "wasRevisionOf": {
      "@id": "prov:wasRevisionOf",
      "@type": "@id"
    },
    "generatedAtTime": {
      "@id": "prov:generatedAtTime",
      "@type": "xsd:dateTime"
    },
    "invalidatedAtTime": {
      "@id": "prov:invalidatedAtTime",
      "@type": "xsd:dateTime"
    },
    "value": "prov:value",
    "qualifiedPrimarySource": {
      "@id": "prov:qualifiedPrimarySource",
      "@type": "@id"
    },
    "qualifiedQuotation": {
      "@id": "prov:qualifiedQuotation",
      "@type": "@id"
    },
    "qualifiedRevision": {
      "@id": "prov:qualifiedRevision",
      "@type": "@id"
    },
    "atLocation": {
      "@id": "prov:atLocation",
      "@type": "@id"
    },
    "links": {
      "@context": {
        "href": {
          "@type": "@id",
          "@id": "oa:hasTarget"
        },
        "rel": {
          "@context": {
            "@base": "http://www.iana.org/assignments/relation/"
          },
          "@id": "http://www.iana.org/assignments/relation",
          "@type": "@id"
        },
        "type": "dct:type",
        "hreflang": "dct:language",
        "title": "rdfs:label",
        "length": "dct:extent"
      },
      "@id": "rdfs:seeAlso"
    },
    "qualifiedGeneration": {
      "@id": "prov:qualifiedGeneration",
      "@type": "@id"
    },
    "qualifiedInvalidation": {
      "@id": "prov:qualifiedInvalidation",
      "@type": "@id"
    },
    "qualifiedDerivation": {
      "@id": "prov:qualifiedDerivation",
      "@type": "@id"
    },
    "qualifiedAttribution": {
      "@id": "prov:qualifiedAttribution",
      "@type": "@id"
    },
    "activityType": "@type",
    "agentType": "@type",
    "Activity": "prov:Activity",
    "ActivityInfluence": "prov:ActivityInfluence",
    "Agent": "prov:Agent",
    "AgentInfluence": "prov:AgentInfluence",
    "Association": "prov:Association",
    "Attribution": "prov:Attribution",
    "Bundle": "prov:Bundle",
    "Collection": "prov:Collection",
    "Communication": "prov:Communication",
    "Delegation": "prov:Delegation",
    "Derivation": "prov:Derivation",
    "EmptyCollection": "prov:EmptyCollection",
    "End": "prov:End",
    "Entity": "prov:Entity",
    "EntityInfluence": "prov:EntityInfluence",
    "Generation": "prov:Generation",
    "Influence": "prov:Influence",
    "InstantaneousEvent": "prov:InstantaneousEvent",
    "Invalidation": "prov:Invalidation",
    "Location": "prov:Location",
    "Organization": "prov:Organization",
    "Person": "prov:Person",
    "Plan": "prov:Plan",
    "PrimarySource": "prov:PrimarySource",
    "Quotation": "prov:Quotation",
    "Revision": "prov:Revision",
    "Role": "prov:Role",
    "SoftwareAgent": "prov:SoftwareAgent",
    "Start": "prov:Start",
    "Usage": "prov:Usage",
    "ServiceDescription": "prov:ServiceDescription",
    "DirectQueryService": "prov:DirectQueryService",
    "Accept": "prov:Accept",
    "Contribute": "prov:Contribute",
    "Contributor": "prov:Contributor",
    "Copyright": "prov:Copyright",
    "Create": "prov:Create",
    "Creator": "prov:Creator",
    "Modify": "prov:Modify",
    "Publish": "prov:Publish",
    "Publisher": "prov:Publisher",
    "Replace": "prov:Replace",
    "RightsAssignment": "prov:RightsAssignment",
    "RightsHolder": "prov:RightsHolder",
    "Submit": "prov:Submit",
    "Dictionary": "prov:Dictionary",
    "EmptyDictionary": "prov:EmptyDictionary",
    "KeyEntityPair": "prov:KeyEntityPair",
    "Insertion": "prov:Insertion",
    "Removal": "prov:Removal",
    "atTime": {
      "@id": "prov:atTime",
      "@type": "xsd:dateTime"
    },
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "startedAtTime": {
      "@id": "prov:startedAtTime",
      "@type": "xsd:dateTime"
    },
    "provenanceUriTemplate": "prov:provenanceUriTemplate",
    "pairKey": {
      "@id": "prov:pairKey",
      "@type": "rdfs:Literal"
    },
    "removedKey": {
      "@id": "prov:removedKey",
      "@type": "rdfs:Literal"
    },
    "actedOnBehalfOf": {
      "@id": "prov:actedOnBehalfOf",
      "@type": "@id"
    },
    "agent": {
      "@id": "prov:agent",
      "@type": "@id"
    },
    "entity": {
      "@id": "prov:entity",
      "@type": "@id"
    },
    "generated": {
      "@id": "prov:generated",
      "@type": "@id"
    },
    "hadActivity": {
      "@id": "prov:hadActivity",
      "@type": "@id"
    },
    "activity": {
      "@id": "prov:activity",
      "@type": "@id"
    },
    "hadGeneration": {
      "@id": "prov:hadGeneration",
      "@type": "@id"
    },
    "hadPlan": {
      "@id": "prov:hadPlan",
      "@type": "@id"
    },
    "hadRole": {
      "@id": "prov:hadRole",
      "@type": "@id"
    },
    "hadUsage": {
      "@id": "prov:hadUsage",
      "@type": "@id"
    },
    "influenced": {
      "@id": "prov:influenced",
      "@type": "@id"
    },
    "influencer": {
      "@id": "prov:influencer",
      "@type": "@id"
    },
    "invalidated": {
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "qualifiedCommunication": {
      "@id": "prov:qualifiedCommunication",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedStart": {
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedUsage": {
      "@id": "prov:qualifiedUsage",
      "@type": "@id"
    },
    "used": {
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasAssociatedWith": {
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "wasInformedBy": {
      "@id": "prov:wasInformedBy",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "has_anchor": {
      "@id": "prov:has_anchor",
      "@type": "@id"
    },
    "has_query_service": {
      "@id": "prov:has_query_service",
      "@type": "@id"
    },
    "describesService": {
      "@id": "prov:describesService",
      "@type": "@id"
    },
    "pingback": {
      "@id": "prov:pingback",
      "@type": "@id"
    },
    "dictionary": {
      "@id": "prov:dictionary",
      "@type": "@id"
    },
    "derivedByInsertionFrom": {
      "@id": "prov:derivedByInsertionFrom",
      "@type": "@id"
    },
    "derivedByRemovalFrom": {
      "@id": "prov:derivedByRemovalFrom",
      "@type": "@id"
    },
    "insertedKeyEntityPair": {
      "@id": "prov:insertedKeyEntityPair",
      "@type": "@id"
    },
    "hadDictionaryMember": {
      "@id": "prov:hadDictionaryMember",
      "@type": "@id"
    },
    "pairEntity": {
      "@id": "prov:pairEntity",
      "@type": "@id"
    },
    "qualifiedInsertion": {
      "@id": "prov:qualifiedInsertion",
      "@type": "@id"
    },
    "qualifiedRemoval": {
      "@id": "prov:qualifiedRemoval",
      "@type": "@id"
    },
    "asInBundle": {
      "@id": "prov:asInBundle",
      "@type": "@id"
    },
    "mentionOf": {
      "@id": "prov:mentionOf",
      "@type": "@id"
    },
    "name": "rdfs:label",
    "processType": {
      "@id": "dct:type",
      "@type": "@id"
    },
    "label": "rdfs:label",
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "oa": "http://www.w3.org/ns/oa#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://nsnarayanam.github.io/bblocks-openscience/build/annotated/osc/prov-processing-step/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nsnarayanam/bblocks-openscience](https://github.com/nsnarayanam/bblocks-openscience)
* Path: `_sources/prov-processing-step`

