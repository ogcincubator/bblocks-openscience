
# Custom OGC API processes instance (Api)

`ogc.osc.api-profiles.processes.sample-implementation` *v1.0*

An example of an OGC API Processes implementation using the extension point mechanism for complex Building Blocks

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Custom OGC API - Processes instance

This building block is a worked example of **profiling an OGC API** with OGC Building Blocks. It describes a
concrete OGC API - Processes 1.0 implementation that exposes a single, fixed process (`buffer-geometry`),
built by specialising the generic [OGC API - Processes](https://ogcapi.ogc.org/processes/) base building block
`ogc.api.processes.v1.api` rather than copying it.

It is intended as a template for other API profiles in this register (for example the IPT, OSPD and workflow
profiles).

### How the profile is built

The profile combines two mechanisms:

1. **`isProfileOf`** declares that this API is a profile of `ogc.api.processes.v1.api`, making the
   relationship discoverable in the register.
2. **`extensionPoints`** substitutes generic schema components of the base with process-specific ones:

   | Base component (extension point) | Replaced by |
   |---|---|
   | `ogc.api.processes.v1.schemas.inputDescription` | `…sample-implementation.schemas.inputDescriptions` |
   | `ogc.api.processes.v1.schemas.outputDescription` | `…sample-implementation.schemas.outputDescriptions` |
   | `ogc.api.processes.v1.schemas.results` | `…sample-implementation.schemas.buffer-geometry.outputSchema` |

   The `inputDescriptions` / `outputDescriptions` blocks are thin `anyOf` collections of process-specific
   descriptions. Mapping the extension point to a collection, rather than directly to the `buffer-geometry`
   descriptions, keeps the extension point stable: further processes can be added by extending the collection
   without touching this block's metadata.

The profile's own `openapi.yaml` is written in **overlay style**: it only declares what differs from the base.
The postprocessor merges it into the base OpenAPI document:

- the generic `/processes/{processID}` and `/processes/{processID}/execution` paths are removed (set to `false`)
  and replaced by the concrete `/processes/buffer-geometry` and `/processes/buffer-geometry/execution` paths;
- all other base paths (`/`, `/conformance`, `/processes`, `/jobs`, …) are inherited unchanged, with the
  extension point substitutions applied automatically wherever the base references the substituted schemas
  (e.g. the job results response).

### Component building blocks

| Block | Role |
|---|---|
| `schemas.buffer-geometry.inputSchema` / `outputSchema` | Data shape of the process inputs and outputs |
| `schemas.buffer-geometry.inputDescription` / `outputDescription` | Specialise the base's generic input/output descriptions for `buffer-geometry` |
| `schemas.buffer-geometry.processDescription` | Composes the base process schema with the two description blocks |
| `schemas.inputDescriptions` / `outputDescriptions` | `anyOf` collections of known process descriptions — the extension point targets |

### Documentation on extension points and profiling

- [Extension points](https://ogcincubator.github.io/bblocks-docs/create/extension-points) — the
  `extensionPoints` mechanism, including how OpenAPI-backed building blocks are merged (path overrides,
  `false` removals, whole-value overrides of `info`/`servers`/`tags`) and its limitations (e.g. no `#`
  fragment targets). Note this feature is experimental; inspect the compiled output.
- [Profiling an API](https://ogcincubator.github.io/bblocks-docs/usecases/api-profiling) — step-by-step
  walkthrough of this OGC API - Processes example and the rationale for its structure.
- [Profiles](https://ogcincubator.github.io/bblocks-docs/overview/profiles) — the general concept of
  profiles and the `isProfileOf` relationship.
- [Relationships](https://ogcincubator.github.io/bblocks-docs/overview/relationships) — how building blocks
  relate to each other (dependencies, profiles, extensions).
- [Setting up imports](https://ogcincubator.github.io/bblocks-docs/create/imports) — importing external
  registers such as the one providing `ogc.api.processes.v1.*`.
- [Building Block metadata](https://ogcincubator.github.io/bblocks-docs/create/metadata) — `bblock.json`
  fields, including `isProfileOf` and `extensionPoints`.


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-openscience](https://github.com/ogcincubator/bblocks-openscience)
* Path: `_sources/api-profiles/processes/sample-implementation`

