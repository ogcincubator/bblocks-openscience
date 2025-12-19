
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

* YAML version: [schema.yaml](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/ipt/execute/schema.json)
* JSON version: [schema.json](https://nenadradosevic.github.io/bblocks-openscience/build/annotated/osc/api-profiles/processes/ipt/execute/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nenadradosevic/bblocks-openscience](https://github.com/nenadradosevic/bblocks-openscience)
* Path: `_sources/api-profiles/processes/ipt/execute`

