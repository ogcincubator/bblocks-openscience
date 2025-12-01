
# IPT Profile of OGC API Processes (Api)

`ogc.osc.api-profiles.processes.ipt.api` *v0.1*

This is a Profile of the OGC API Processes model with specific requirements to standardise Integrity Provenance and Trust (IPT) aspects/

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## IPT Profile

The IPT profile supports canonical mechanisms for handling Integrity, Provenance and Trust.

Specifically this profile:

1. allows a client to nominate IRI identifier for the prov:Activity
2. allows a client to nominate IRI for the Process Service as an prov:Agent
3. allows a client to nominate an IRI for the result object
4. Defines how a provenance trace can be return by reference or inline in the result as a prov:Entity

These constraints are defined by specialisations of input and output descriptions.

Todo: define how the OpenAPI document refines the base.
## Sources

* [OGC API Processes](https://docs.ogc.org/is/18-062r2/18-062r2.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ahaywardtvuk/bblocks-openscience](https://github.com/ahaywardtvuk/bblocks-openscience)
* Path: `_sources/api-profiles/processes/ipt/api`

