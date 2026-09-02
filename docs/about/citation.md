# Citation

## Cite openair (the science)

Charts and statistics are produced by the **[openair](https://github.com/openair-project/openair)** R package (MIT). In papers, reports, or published figures, cite openair itself, not this wrapper:

> Carslaw, D. C. and K. Ropkins (2012). *openair — an R package for air quality data analysis.* Environmental Modelling & Software, 27–28, 52–61. [doi:10.1016/j.envsoft.2011.09.008](https://doi.org/10.1016/j.envsoft.2011.09.008)

BibTeX and updates: [openair citation page](https://openair-project.github.io/openair/authors.html). In R: `citation("openair")`.

## Cite this kit (the wrapper, optional)

You do not need permission to use either repo, commercially or not — both are MIT. If this MCP kit was part of your workflow and you publish methods, a brief mention or link is appreciated, but **the scientific citation is openair**, not this wrapper.

Each repo carries a machine-readable `CITATION.cff` (GitHub renders a "Cite this repository" button on both):

- [openair-3-mcp-server-oss/CITATION.cff](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/CITATION.cff)
- [openair-3-mcp-client-plugin-oss/CITATION.cff](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/CITATION.cff)

## Public air-quality data

`import_aurn`, `import_europe`, and related tools fetch **third-party datasets**, not data shipped with either repo. Follow each provider's licence when you publish or redistribute results.

| Source | Typical requirement |
|--------|---------------------|
| UK networks (AURN, etc.) | [Open Government Licence](https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) — attribute Defra / [uk-air.defra.gov.uk](https://uk-air.defra.gov.uk/) |
| European networks | Respect source terms — see `import_europe` docs for availability |
| Your own CSV | Your responsibility only |

Example UK data attribution (OGL):

> © Crown copyright Defra via uk-air.defra.gov.uk, licensed under the Open Government Licence.
