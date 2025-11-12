## ESA EarthCODE Products as GeoDCAT and STAC profile 

This building block represents the outputs of an EarthCODE Experiment.

This is a STAC Collection using the themes, osc and cf extensions with some additional EarthCODE-specific fields.

The EarthCODE OSC has requirements which are not captured here

  - A list of conceps following the OSC theme scheme must be present using the themes extension
  - Each theme ID must match the ID of a Catalog at /themes/theme-id/catalog.json
  - A 'related' link must exists in `links` also pointing to the theme Catalog
  - The osc:project, osc:variables, osc:missions and osc:experiment fields should contain the IDs of catalogue entries found at /projects/{id}/collection.json, /variables/{id}/catalog.json, /missions/{id}/catalog.json or /experiments/{id}/record.json repsectively.
