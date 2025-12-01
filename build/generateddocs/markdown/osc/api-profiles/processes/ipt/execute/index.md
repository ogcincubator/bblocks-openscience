
# Execute (request) schema for IPT (Schema)

`ogc.osc.api-profiles.processes.ipt.execute` *v0.1*

None

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-ogcapi-processes/build/annotated/api/processes/v1/schemas/execute/schema.yaml
properties:
  inputs:
    activity_id:
      $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
    result_id:
      $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
    agent_id:
      $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
required:
- activity_id

```

Links to the schema:

* YAML version: [schema.yaml](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/ipt/execute/schema.json)
* JSON version: [schema.json](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/ipt/execute/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "inputs": {
      "@context": {
        "bbox": {},
        "crs": {},
        "encoding": {},
        "mediaType": {},
        "schema": {},
        "value": {},
        "href": {},
        "hreflang": {},
        "rel": {},
        "title": {},
        "type": {}
      }
    },
    "outputs": {
      "@context": {
        "format": {
          "@context": {
            "encoding": {},
            "mediaType": {},
            "schema": {}
          }
        },
        "transmissionMode": {}
      }
    },
    "response": {},
    "subscriber": {
      "@context": {
        "failedUri": {},
        "inProgressUri": {},
        "successUri": {}
      }
    },
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ahaywardtvuk.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/ipt/execute/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ahaywardtvuk/bblocks-openscience](https://github.com/ahaywardtvuk/bblocks-openscience)
* Path: `_sources/api-profiles/processes/ipt/execute`

