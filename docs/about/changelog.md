# Changelog

Each repo keeps its own changelog — they version together, so release notes are easiest to read side by side:

- [openair-3-mcp-server-oss/CHANGELOG.md](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/CHANGELOG.md)
- [openair-3-mcp-client-plugin-oss/CHANGELOG.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/CHANGELOG.md)

## v0.2.1 (2026-11-20) — dist_plot, themes, importMeta filters

Binomio release for openair 3.2 feature parity on the MCP surface.

**Server:** new `dist_plot`; optional `plot_options.theme` / `meta.theme` on all image tools; `import_meta` forwards `importMeta()` 3.2 filters (distance search, pollutants, year, …). **38** R-backed tools.

**Plugin:** skills and plot catalog updated (`prepare-plot`, `ingest-network`).

Hosted users: pull tags **v0.2.1** on server and plugin; `health_r` after deploy completes.

## v0.2.0 (2026-11-20) — openair 3.2.0 on the server host

Binomio release aligned with **[openair 3.2.0 on CRAN](https://cran.r-project.org/package=openair)** (2026-11-19). No new MCP tools in this release.

**Server host (R):** install or upgrade `openair >= 3.2.0` and `legendry >= 0.3.0`, then run `health_r`. Hosted users on `mcp.miguel-escribano.com` — server R is upgraded; update the Claude/Cursor plugin to match release tags when convenient.

**Plugin:** doc and version bump only; skills unchanged.

## v0.1.0 (2026-06-30) — initial public release

The first public release of the binomio: CSV/Excel/upload ingest (with optional `lat`/`lon` for future `worldmet` support), public-network imports (AURN, EU, UK AQ networks), the full openair plot/stats surface (37 R-backed tools), the `openair-agent` persona with routing guardrails, and the Felisa `WindSeriesV1` golden fixture backing a 16-check acceptance harness.

See the [Roadmap in the server README](https://github.com/miguel-escribano/openair-3-mcp-server-oss#roadmap) for what's planned next (`worldmet`, `openairmaps`, `deweather`).
