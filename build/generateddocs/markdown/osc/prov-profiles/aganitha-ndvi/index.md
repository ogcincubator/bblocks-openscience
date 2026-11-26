
# Geospatial Processing Step Provenance (Schema)

`ogc.osc.prov-profiles.aganitha-ndvi` *v0.1.0*

A profile of the PROV-O building block constrained to the description of a single geospatial processing step, with a required link to a registered process type.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Geospatial Processing Step Provenance

This building block profiles the
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step)
for one geospatial processing step.

PROV-O is deliberately general. Any valid PROV document is a valid description
of a processing step, which makes validation weak and cross-platform comparison
hard.

OGC API - Processes Part 5 (draft 26-038) narrows this for job provenance: a
job entity, a process entity, an activity joining them, and input/output
artifacts carrying roles. This profile follows that shape.

Part 5 does not define any link from a process to a registered process type.
The base profile makes that link required: `provType` is `Activity`, and
`activityType` gives the registered process type. On top of that, this profile adds:

- `used` and `generated` on the activity, as non-empty arrays of entity references;
- a `hadRole` on every `qualifiedUsage`, naming the input slot of the process type;
- step parameters, when given, in a single `parameters` object keyed by the process type's parameter terms.

Under development as part of OSPD 2026, deliverable D104 (Aganitha Space
Technologies, Workflow Profiler).

## Examples

### Ingest of mandal-level vegetation and soil moisture
Retrieval of source observations into the workflow. Ingest is where external provenance ends and workflow provenance begins: the generated entity is the first thing downstream steps can cite.
#### json
```json
{
  "id": "urn:aganitha:step:ingest-dicra:20260807T060000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/GA047",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:ingest-dicra:20260807T060000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/GA047",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<urn:aganitha:step:ingest-dicra:20260807T060000Z> a prov:Activity ;
    rdfs:label "Ingest mandal NDVI and soil moisture" ;
    prov:endedAtTime "2026-08-07T06:03:41+00:00"^^xsd:dateTime ;
    prov:generated <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:source:dicra-mandal-archive> ;
            prov:hadRole <https://example.org/ospd/roles/sourceArchive> ] ;
    prov:startedAtTime "2026-08-07T06:00:00+00:00"^^xsd:dateTime ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/GA047> ;
    prov:used <urn:aganitha:source:dicra-mandal-archive> .


```


### Normalisation of vegetation index to a condition index
Rescaling an observed index against its own historical extremes. The reference extrema are inputs rather than inline constants, so the period they were derived from is recoverable from the provenance.
#### json
```json
{
  "id": "urn:aganitha:step:vci:20260807T061000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:vci:20260807T061000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:vci:20260807T061000Z> a prov:Activity ;
    rdfs:label "Compute vegetation condition index from NDVI" ;
    prov:generated <urn:aganitha:dataset:vci> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:reference:ndvi-extrema> ;
            prov:hadRole <https://example.org/ospd/roles/normalisationReference> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
            prov:hadRole <https://example.org/ospd/roles/observedIndex> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation> ;
    prov:used <urn:aganitha:dataset:mandal-ndvi-sm-merged>,
        <urn:aganitha:reference:ndvi-extrema> .


```


### Normalisation of soil moisture to a deficit index
The companion to the vegetation index step, and the piece that closes the gap in the chain: without it, the combined index consumes an entity no recorded activity produced, so a consumer walking the provenance backwards hits a dead end.
#### json
```json
{
  "id": "urn:aganitha:step:smdi:20260807T061500Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:smdi:20260807T061500Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:smdi:20260807T061500Z> a prov:Activity ;
    rdfs:label "Compute soil moisture deficit index" ;
    prov:generated <urn:aganitha:dataset:smdi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:reference:soil-moisture-extrema> ;
            prov:hadRole <https://example.org/ospd/roles/normalisationReference> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:mandal-ndvi-sm-merged> ;
            prov:hadRole <https://example.org/ospd/roles/observedIndex> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/aganitha-index-normalisation> ;
    prov:used <urn:aganitha:dataset:mandal-ndvi-sm-merged>,
        <urn:aganitha:reference:soil-moisture-extrema> .


```


### Weighted composition of a combined drought index
Combination of two condition indices under fixed weights. Both inputs share the same role, and the weights are step parameters rather than properties of the process type — a case that bears directly on how finely process types should be registered.
#### json
```json
{
  "id": "urn:aganitha:step:cdsi:20260807T062000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/index-composition",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:cdsi:20260807T062000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/index-composition",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:cdsi:20260807T062000Z> a prov:Activity ;
    rdfs:label "Compose combined drought severity index" ;
    prov:generated <urn:aganitha:dataset:cdsi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:vci> ;
            prov:hadRole <https://example.org/ospd/roles/indexComponent> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:smdi> ;
            prov:hadRole <https://example.org/ospd/roles/indexComponent> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/index-composition> ;
    prov:used <urn:aganitha:dataset:smdi>,
        <urn:aganitha:dataset:vci> .


```


### Classification into drought severity classes
Assignment of continuous index values to discrete classes. The class scheme is an input entity, so the thresholds applied are recoverable from the provenance without reading the code.
#### json
```json
{
  "id": "urn:aganitha:step:classify:20260807T063000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-drought-classification",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:classify:20260807T063000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-drought-classification",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:classify:20260807T063000Z> a prov:Activity ;
    rdfs:label "Classify drought severity" ;
    prov:generated <urn:aganitha:dataset:drought-classes> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:scheme:drought-severity-classes> ;
            prov:hadRole <https://example.org/ospd/roles/classificationScheme> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/inputField> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/aganitha-drought-classification> ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:scheme:drought-severity-classes> .


```


### Standardised precipitation index over an accumulation window
Derivation of a standardised index from an accumulated series against a fitted reference period. Two entities of the same kind distinguished only by role — the case where entity references alone would be ambiguous and qualifiedUsage does real work.
#### json
```json
{
  "id": "urn:aganitha:step:spi:20260807T064000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-standardised-index",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:spi:20260807T064000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/aganitha-standardised-index",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:spi:20260807T064000Z> a prov:Activity ;
    rdfs:label "Compute standardised precipitation index" ;
    prov:generated <urn:aganitha:dataset:spi> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:precipitation-reference-period> ;
            prov:hadRole <https://example.org/ospd/roles/fittingReference> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:precipitation-series> ;
            prov:hadRole <https://example.org/ospd/roles/inputSeries> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/aganitha-standardised-index> ;
    prov:used <urn:aganitha:dataset:precipitation-reference-period>,
        <urn:aganitha:dataset:precipitation-series> .


```


### Model training as a processing step
Training a predictive model, expressed as an ordinary processing activity. The generated entity is a fitted model rather than a data product, and the fold assignment is an input entity so the spatial cross-validation design is recoverable from the provenance.
This is the case the profile is least obviously shaped for, and the reason it is included: if a trained model cannot be expressed as an entity generated by an activity, the profile cannot describe machine learning workflows at all.
#### json
```json
{
  "id": "urn:aganitha:step:train:20260807T070000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/model-training",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:train:20260807T070000Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/model-training",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:train:20260807T070000Z> a prov:Activity ;
    rdfs:label "Train drought prediction model with spatial cross-validation" ;
    prov:generated <urn:aganitha:model:drought-classifier>,
        <urn:aganitha:report:validation-metrics> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:drought-classes> ;
            prov:hadRole <https://example.org/ospd/roles/trainingTarget> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:partition:district-folds> ;
            prov:hadRole <https://example.org/ospd/roles/validationPartition> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:spi> ;
            prov:hadRole <https://example.org/ospd/roles/trainingFeatures> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/trainingFeatures> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/model-training> ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:dataset:drought-classes>,
        <urn:aganitha:dataset:spi>,
        <urn:aganitha:partition:district-folds> .


```


### Inference using a trained model
Applying a fitted model to produce a projection. The same model entity that was generated by training is here consumed as an input — the round trip that makes model provenance chainable, and something no purely data-oriented profile has to handle.
#### json
```json
{
  "id": "urn:aganitha:step:project:20260807T071500Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/model-inference",
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
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:aganitha:step:project:20260807T071500Z",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/model-inference",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:aganitha:step:project:20260807T071500Z> a prov:Activity ;
    rdfs:label "Generate forward drought projection" ;
    prov:generated <urn:aganitha:dataset:drought-projection> ;
    prov:qualifiedUsage [ a prov:Usage ;
            prov:entity <urn:aganitha:dataset:cdsi> ;
            prov:hadRole <https://example.org/ospd/roles/inferenceInput> ],
        [ a prov:Usage ;
            prov:entity <urn:aganitha:model:drought-classifier> ;
            prov:hadRole <https://example.org/ospd/roles/fittedModel> ] ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/model-inference> ;
    prov:used <urn:aganitha:dataset:cdsi>,
        <urn:aganitha:model:drought-classifier> .


```


### Minimal conforming step
The smallest document that satisfies this profile.
#### json
```json
{
  "id": "urn:example:step:0001",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/GA047",
  "label": "Minimal step",
  "used": ["urn:example:input:0001"],
  "generated": ["urn:example:output:0001"]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld",
  "id": "urn:example:step:0001",
  "provType": "Activity",
  "activityType": "https://w3id.org/ogc/ospd/activity-type/GA047",
  "label": "Minimal step",
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
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:example:step:0001> a prov:Activity ;
    rdfs:label "Minimal step" ;
    prov:generated <urn:example:output:0001> ;
    prov:type <https://w3id.org/ogc/ospd/activity-type/GA047> ;
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
- $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/processing-step/schema.yaml
- type: object
  required:
  - used
  - generated
  properties:
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
          hadRole:
            type: string
    parameters:
      description: 'Parameter values that determined the behaviour of this step. Keys
        SHOULD be drawn from the parameter terms declared by the registered process
        type. Deliberately left unbound in the JSON-LD context: how parameters should
        be typed depends on whether process types are registered coarsely or as parameterised
        subtypes, which is still an open question for the register design.'
      type: object
      additionalProperties: true
x-bblocks-metadata:
  itemIdentifier: ogc.osc.prov-profiles.aganitha-ndvi
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: 0.1.0
  dateOfLastChange: '2026-08-05'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasInfluencedBy": {
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
      "@id": "prov:wasInfluencedBy",
      "@type": "@id"
    },
    "qualifiedInfluence": {
      "@context": {
        "influencer": {
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
          "@id": "prov:influencer",
          "@type": "@id"
        },
        "entity": {
          "@context": {
            "wasAttributedTo": {
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
              "@id": "prov:wasAttributedTo",
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
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        },
        "agent": {
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
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedInfluence",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "activityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "name": "rdfs:label",
    "startedAtTime": {
      "@id": "prov:startedAtTime",
      "@type": "xsd:dateTime"
    },
    "endedAtTime": {
      "@id": "prov:endedAtTime",
      "@type": "xsd:dateTime"
    },
    "wasAssociatedWith": {
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
      "@id": "prov:wasAssociatedWith",
      "@type": "@id"
    },
    "wasInformedBy": {
      "@id": "prov:wasInformedBy",
      "@type": "@id"
    },
    "used": {
      "@context": {
        "wasAttributedTo": {
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
          "@id": "prov:wasAttributedTo",
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
        }
      },
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@context": {
        "wasAttributedTo": {
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
          "@id": "prov:wasAttributedTo",
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
        }
      },
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@context": {
        "wasAttributedTo": {
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
          "@id": "prov:wasAttributedTo",
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
        }
      },
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "invalidated": {
      "@context": {
        "wasAttributedTo": {
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
          "@id": "prov:wasAttributedTo",
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
        }
      },
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "generated": {
      "@context": {
        "wasAttributedTo": {
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
          "@id": "prov:wasAttributedTo",
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
        }
      },
      "@id": "prov:generated",
      "@type": "@id"
    },
    "atLocation": {
      "@id": "prov:atLocation",
      "@type": "@id"
    },
    "qualifiedUsage": {
      "@id": "prov:qualifiedUsage",
      "@type": "@id"
    },
    "qualifiedCommunication": {
      "@id": "prov:qualifiedCommunication",
      "@type": "@id"
    },
    "qualifiedStart": {
      "@context": {
        "entity": {
          "@context": {
            "wasAttributedTo": {
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
              "@id": "prov:wasAttributedTo",
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
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@context": {
        "entity": {
          "@context": {
            "wasAttributedTo": {
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
              "@id": "prov:wasAttributedTo",
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
            }
          },
          "@id": "prov:entity",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@context": {
        "agent": {
          "@context": {
            "actedOnBehalfOf": {
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
              "@id": "prov:actedOnBehalfOf",
              "@type": "@id"
            }
          },
          "@id": "prov:agent",
          "@type": "@id"
        }
      },
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "agentType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "entityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "influenceType": {
      "@id": "prov:type",
      "@type": "@id"
    },
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
    "generatedAtTime": {
      "@id": "prov:generatedAtTime",
      "@type": "xsd:dateTime"
    },
    "invalidatedAtTime": {
      "@id": "prov:invalidatedAtTime",
      "@type": "xsd:dateTime"
    },
    "value": "prov:value",
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
    "alternateOf": {
      "@id": "prov:alternateOf",
      "@type": "@id"
    },
    "entity": {
      "@id": "prov:entity",
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
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "hadPlan": {
      "@id": "prov:hadPlan",
      "@type": "@id"
    },
    "hadPrimarySource": {
      "@id": "prov:hadPrimarySource",
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
    "qualifiedAttribution": {
      "@id": "prov:qualifiedAttribution",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
      "@type": "@id"
    },
    "qualifiedDerivation": {
      "@id": "prov:qualifiedDerivation",
      "@type": "@id"
    },
    "qualifiedGeneration": {
      "@id": "prov:qualifiedGeneration",
      "@type": "@id"
    },
    "qualifiedInvalidation": {
      "@id": "prov:qualifiedInvalidation",
      "@type": "@id"
    },
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
    "specializationOf": {
      "@id": "prov:specializationOf",
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
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
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
    "links": "rdfs:seeAlso",
    "label": "rdfs:label",
    "prov": "http://www.w3.org/ns/prov#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "rdfs": "http://www.w3.org/2000/01/rdf-schema#",
    "dct": "http://purl.org/dc/terms/",
    "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
    "foaf": "http://xmlns.com/foaf/0.1/",
    "schema": "https://schema.org/",
    "wfprov": "http://purl.org/wf4ever/wfprov#",
    "wfdesc": "http://purl.org/wf4ever/wfdesc#",
    "wf4ever": "http://purl.org/wf4ever/wf4ever#",
    "oa": "http://www.w3.org/ns/oa#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/aganitha-ndvi/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/prov-profiles/aganitha-ndvi`

