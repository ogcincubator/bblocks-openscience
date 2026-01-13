
# Buffer geometry process input schema (Schema)

`ogc.osc.ogcapi-processes.profiled-api.schemas.buffer-geometry.inputSchema` *v1.0*

Input schema for the buffer geometry process

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
type: object
required:
- geometry
- distance
properties:
  geometry:
    allOf:
    - $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/geo/common/data_types/geojson/schema.yaml
    - required:
      - type
      - coordinates
      properties:
        type:
          enum:
          - Point
          - LineString
          - polygon
  distance:
    type: object
    properties:
      type:
        type: string
        example: number
      minimum:
        type: number
        example: 0
  units:
    $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
    enum:
    - meters
    - kilometers
    - feet
    - miles
    default: meters

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/ogcapi-processes/profiled-api/schemas/buffer-geometry/inputSchema/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/ogcapi-processes/profiled-api/schemas/buffer-geometry/inputSchema/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Feature": "geojson:Feature",
    "FeatureCollection": "geojson:FeatureCollection",
    "GeometryCollection": "geojson:GeometryCollection",
    "LineString": "geojson:LineString",
    "MultiLineString": "geojson:MultiLineString",
    "MultiPoint": "geojson:MultiPoint",
    "MultiPolygon": "geojson:MultiPolygon",
    "Point": "geojson:Point",
    "Polygon": "geojson:Polygon",
    "features": {
      "@container": "@set",
      "@id": "geojson:features"
    },
    "type": "@type",
    "id": "@id",
    "properties": "@nest",
    "geometry": {
      "@context": {
        "coordinates": {
          "@container": "@list",
          "@id": "geojson:coordinates"
        }
      },
      "@id": "geojson:geometry"
    },
    "bbox": {
      "@container": "@list",
      "@id": "geojson:bbox"
    },
    "geojson": "https://purl.org/geojson/vocab#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-openscience/build/annotated/osc/ogcapi-processes/profiled-api/schemas/buffer-geometry/inputSchema/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/ogcapi-processes/profiled-api/schemas/buffer-geometry/inputSchema`

