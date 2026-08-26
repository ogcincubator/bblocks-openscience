
# Buffer geometry process output schema (Schema)

`ogc.osc.api-profiles.processes.sample-implementation.schemas.buffer-geometry.outputSchema` *v1.0*

Output schema for the buffer geometry process

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
type: object
properties:
  bufferedGeometry:
    type: object
    properties:
      type:
        type: string
        const: Polygon
      coordinates:
        type: array
        minItems: 2
        items:
          type: number
  area:
    type: number
    minimum: 0

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputSchema/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/nsnarayanam/bblocks-openscience/undefined/build/annotated/osc/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputSchema/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/nsnarayanam/bblocks-openscience](https://github.com/nsnarayanam/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation/schemas/buffer-geometry/outputSchema`

