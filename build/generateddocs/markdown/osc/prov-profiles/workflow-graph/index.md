
# Workflow Provenance Graph (Schema)

`ogc.osc.prov-profiles.workflow-graph` *v0.1.0*

Provenance of a workflow run as a PROV graph in which every activity is a registered processing step.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

# Workflow Provenance Graph

Provenance of one workflow run, in either of two forms:

- **Graph form**: a JSON array of PROV entities, activities and agents (the
  pattern used by the 52°North workflow provenance examples).
- **Bundle form**: a single entity whose `entityType` (or `@type`) includes
  `prov:Bundle`, with its nodes nested inside it, at any depth and under any
  property names (the pattern used by the HARTIS CVI workflow).

In both forms, every object that is a PROV Activity (its `provType` or
`@type` includes `Activity`, or it has an `activityType`) must conform to the
[Registered Processing Step](bblock://ogc.osc.prov-profiles.processing-step)
profile, wherever it sits in the document (`@context` is skipped). Each step
in the run is therefore typed by a process type from a governed register,
which is what makes two runs of a workflow, on different platforms,
comparable step by step.

Reusable descriptions should have a human-readable label: plans (including
workflow definitions) and agents. A missing label is reported as a warning. Other entities need not be labelled, as
they may be temporary artefacts passed between activities; nor need the
records of an individual run, the activities and the bundle that holds a
run. The process types that `activityType` points to are labelled in their
register.

The label requirement is checked by SHACL on the uplifted graph
(`rdfs:label`), not by the JSON schema, so a label can be generated during
semantic uplift. This block's uplift rule (`uplift/labels.shacl`) derives
`rdfs:label` from `dcterms:title` or `skos:prefLabel` when no label is given;
profiles can add their own label-generation rules.

`provType` identifies the PROV class of each node (`Entity`, `Activity` or
`Agent`); `entityType`, `activityType` and `agentType` then only carry the
specific types, as IRIs or CURIEs.

Outputs are commonly stated from the entity side (`wasGeneratedBy`); the
processing-step SHACL shapes accept either direction.

### Type uplift

The PROV building blocks map `entityType`, `activityType` and `agentType` to `prov:type`; only
`provType` gives `rdf:type`. Before validation, this block's uplift rule (`uplift/types.shacl`)
also asserts `rdf:type` for an allow-list of classes: the PROV subclasses (`prov:Plan`,
`prov:Bundle`, `prov:Collection`, `prov:EmptyCollection`, `prov:Person`, `prov:Organization`,
`prov:SoftwareAgent`) and the activity-type register's `acttype:WorkflowPlan`,
`acttype:WorkflowRun` and `acttype:WorkflowRunner`. This lets the label shapes target plans and
agents by class.

Process types are not copied: they remain `prov:type` values, so that a run does not become an
instance of a register item class. Shapes about process types should select nodes by their
`prov:type` value.

## Examples

### Two-step workflow run
An input entity, two registered steps, and the outputs, with generation stated from the entity side. provType identifies each node's PROV class; activityType gives each step its registered process type.
#### json
```json
[
  {
    "id": "urn:example:dataset:areas-wgs84",
    "provType": "Entity",
    "rdfs:label": "Green areas (WGS 84)"
  },
  {
    "id": "urn:example:step:reproject",
    "provType": "Activity",
    "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018",
    "rdfs:label": "Reproject green areas",
    "used": "urn:example:dataset:areas-wgs84"
  },
  {
    "id": "urn:example:dataset:areas-utm32n",
    "provType": "Entity",
    "rdfs:label": "Green areas (UTM 32N)",
    "wasGeneratedBy": "urn:example:step:reproject"
  },
  {
    "id": "urn:example:step:buffer",
    "provType": "Activity",
    "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA020",
    "rdfs:label": "Buffer green areas by 300 m",
    "used": "urn:example:dataset:areas-utm32n"
  },
  {
    "id": "urn:example:dataset:areas-buffered",
    "provType": "Entity",
    "rdfs:label": "Buffered green areas",
    "wasGeneratedBy": "urn:example:step:buffer"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/context.jsonld",
  "@graph": [
    {
      "id": "urn:example:dataset:areas-wgs84",
      "provType": "Entity",
      "rdfs:label": "Green areas (WGS 84)"
    },
    {
      "id": "urn:example:step:reproject",
      "provType": "Activity",
      "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018",
      "rdfs:label": "Reproject green areas",
      "used": "urn:example:dataset:areas-wgs84"
    },
    {
      "id": "urn:example:dataset:areas-utm32n",
      "provType": "Entity",
      "rdfs:label": "Green areas (UTM 32N)",
      "wasGeneratedBy": "urn:example:step:reproject"
    },
    {
      "id": "urn:example:step:buffer",
      "provType": "Activity",
      "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA020",
      "rdfs:label": "Buffer green areas by 300 m",
      "used": "urn:example:dataset:areas-utm32n"
    },
    {
      "id": "urn:example:dataset:areas-buffered",
      "provType": "Entity",
      "rdfs:label": "Buffered green areas",
      "wasGeneratedBy": "urn:example:step:buffer"
    }
  ]
}
```

#### ttl
```ttl
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:example:dataset:areas-buffered> a prov:Entity ;
    rdfs:label "Buffered green areas" ;
    prov:wasGeneratedBy <urn:example:step:buffer> .

<urn:example:dataset:areas-utm32n> a prov:Entity ;
    rdfs:label "Green areas (UTM 32N)" ;
    prov:wasGeneratedBy <urn:example:step:reproject> .

<urn:example:dataset:areas-wgs84> a prov:Entity ;
    rdfs:label "Green areas (WGS 84)" .

<urn:example:step:buffer> a prov:Activity ;
    rdfs:label "Buffer green areas by 300 m" ;
    prov:type <https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA020> ;
    prov:used <urn:example:dataset:areas-utm32n> .

<urn:example:step:reproject> a prov:Activity ;
    rdfs:label "Reproject green areas" ;
    prov:type <https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018> ;
    prov:used <urn:example:dataset:areas-wgs84> .


```


### Workflow run as a bundle
The same kind of run in bundle form: one entity typed prov:Bundle whose steps are nested inside it. The profile finds activities at any depth.
#### json
```json
{
  "id": "urn:example:run:42",
  "provType": "Entity",
  "entityType": "prov:Bundle",
  "rdfs:label": "Cool spot run 42",
  "steps": [
    {
      "id": "urn:example:run:42:reproject",
      "provType": "Activity",
      "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018",
      "rdfs:label": "Reproject green areas",
      "used": "urn:example:dataset:areas-wgs84",
      "generated": "urn:example:dataset:areas-utm32n"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/context.jsonld",
  "id": "urn:example:run:42",
  "provType": "Entity",
  "entityType": "prov:Bundle",
  "rdfs:label": "Cool spot run 42",
  "steps": [
    {
      "id": "urn:example:run:42:reproject",
      "provType": "Activity",
      "activityType": "https://catalog.ospd.dev.kurrawong.ai/catalogs/demo:geoacs/collections/demo:ospd-geoacs/items/demo:GA018",
      "rdfs:label": "Reproject green areas",
      "used": "urn:example:dataset:areas-wgs84",
      "generated": "urn:example:dataset:areas-utm32n"
    }
  ]
}
```

#### ttl
```ttl
@prefix prov: <http://www.w3.org/ns/prov#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

<urn:example:run:42> a prov:Bundle,
        prov:Entity ;
    rdfs:label "Cool spot run 42" ;
    prov:type prov:Bundle .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Workflow Provenance Graph
description: A workflow run expressed either as an array of PROV entities, activities
  and agents (graph form), or as a single prov:Bundle entity that contains them (bundle
  form). Every activity, at any depth in the document, must be a Registered Processing
  Step. Labels on plans and agents are recommended; the SHACL shapes check them after
  semantic uplift and report a missing label as a warning.
allOf:
- $ref: https://ogcincubator.github.io/bblock-prov-schema/build/annotated/ogc-utils/prov/schema.yaml
- anyOf:
  - title: Graph form
    description: A top-level array of PROV nodes, at least one of them an activity.
    type: array
    minItems: 1
    contains:
      $ref: '#/$defs/isActivity'
  - title: Bundle form
    description: A single entity whose entityType (or @type) includes prov:Bundle;
      its nodes may be nested at any depth.
    type: object
    required:
    - id
    anyOf:
    - required:
      - entityType
      properties:
        entityType:
          $ref: '#/$defs/includesBundle'
    - required:
      - '@type'
      properties:
        '@type':
          $ref: '#/$defs/includesBundle'
- $ref: '#/$defs/node'
$defs:
  includesActivity:
    anyOf:
    - enum:
      - Activity
      - prov:Activity
      - http://www.w3.org/ns/prov#Activity
    - type: array
      contains:
        enum:
        - Activity
        - prov:Activity
        - http://www.w3.org/ns/prov#Activity
  includesBundle:
    allOf:
    - $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml#/$defs/Multiple
    - anyOf:
      - enum:
        - Bundle
        - prov:Bundle
        - http://www.w3.org/ns/prov#Bundle
      - type: array
        contains:
          enum:
          - Bundle
          - prov:Bundle
          - http://www.w3.org/ns/prov#Bundle
  isActivity:
    description: 'An object that is a prov:Activity: its provType (or @type) includes
      Activity, or it has an activityType.'
    type: object
    anyOf:
    - required:
      - provType
      properties:
        provType:
          $ref: '#/$defs/includesActivity'
    - required:
      - activityType
    - required:
      - '@type'
      properties:
        '@type':
          $ref: '#/$defs/includesActivity'
  node:
    description: 'Walks the whole document: every activity found, at any depth, must
      conform to the Registered Processing Step profile. @context is skipped.'
    if:
      $ref: '#/$defs/isActivity'
    then:
      $ref: https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/processing-step/schema.yaml
    properties:
      '@context': true
    additionalProperties:
      $ref: '#/$defs/node'
    items:
      $ref: '#/$defs/node'
x-jsonld-prefixes:
  dcterms: http://purl.org/dc/terms/
  skos: http://www.w3.org/2004/02/skos/core#
  acttype: https://w3id.org/ogc/rim/activity-type/
x-bblocks-metadata:
  itemIdentifier: ogc.osc.prov-profiles.workflow-graph
  register: https://ogcincubator.github.io/bblocks-openscience/build/register.json
  version: 0.1.0
  dateOfLastChange: '2026-11-24'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/schema.yaml)


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
    "hadMember": {
      "@id": "prov:hadMember",
      "@type": "@id"
    },
    "id": "@id",
    "provType": "@type",
    "entityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "name": "rdfs:label",
    "wasGeneratedBy": {
      "@id": "prov:wasGeneratedBy",
      "@type": "@id"
    },
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
    "activityType": {
      "@id": "prov:type",
      "@type": "@id"
    },
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
      "@id": "prov:used",
      "@type": "@id"
    },
    "wasStartedBy": {
      "@id": "prov:wasStartedBy",
      "@type": "@id"
    },
    "wasEndedBy": {
      "@id": "prov:wasEndedBy",
      "@type": "@id"
    },
    "invalidated": {
      "@id": "prov:invalidated",
      "@type": "@id"
    },
    "generated": {
      "@id": "prov:generated",
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
      "@id": "prov:qualifiedStart",
      "@type": "@id"
    },
    "qualifiedEnd": {
      "@id": "prov:qualifiedEnd",
      "@type": "@id"
    },
    "qualifiedAssociation": {
      "@id": "prov:qualifiedAssociation",
      "@type": "@id"
    },
    "agentType": {
      "@id": "prov:type",
      "@type": "@id"
    },
    "actedOnBehalfOf": {
      "@id": "prov:actedOnBehalfOf",
      "@type": "@id"
    },
    "qualifiedDelegation": {
      "@id": "prov:qualifiedDelegation",
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
    "provenanceUriTemplate": "prov:provenanceUriTemplate",
    "pairKey": {
      "@id": "prov:pairKey",
      "@type": "rdfs:Literal"
    },
    "removedKey": {
      "@id": "prov:removedKey",
      "@type": "rdfs:Literal"
    },
    "agent": {
      "@id": "prov:agent",
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
    "influenceType": {
      "@id": "prov:type",
      "@type": "@id"
    },
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
    "dcterms": "http://purl.org/dc/terms/",
    "skos": "http://www.w3.org/2004/02/skos/core#",
    "acttype": "https://w3id.org/ogc/rim/activity-type/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/prov-profiles/workflow-graph/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/prov-profiles/workflow-graph`

