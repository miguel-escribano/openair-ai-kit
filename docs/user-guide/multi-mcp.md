# Chaining another MCP

Already have a REST API, a Postgres read MCP, an Airtable MCP, or a custom sensor pipeline exposed as an MCP tool? Chain it into openair instead of re-implementing ingest.

1. Configure the **second MCP** in your client alongside `openair-3-mcp` — see [CONNECTORS.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/CONNECTORS.md).
2. Call the upstream tool that returns hourly/time-series JSON.
3. `prepare_series_for_openair(json_exports=[export])` — optional `series_name`, `parameter`, `granularity`, `timezone_name`.
4. A plot tool.

The upstream MCP owns fetch and query; `openair-3-mcp` owns alignment and the openair plots. Neither reimplements the other.

## What the export must look like

`json_exports` must be structured JSON matching `series_v1`, or a compatible bucketed `parameters[].data` layout — see [`export_bridge.py`](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/openair_mcp/export_bridge.py) and the [`series.v1.json` schema](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/schemas/series.v1.json). Never build the array by hand in chat — pass through whatever the upstream MCP already returned.

## When you don't need this

Standalone CSV, Excel, or `import_*` users never need a second MCP — this pattern is only for data that already lives behind a *different* tool you want to keep using as the source of truth.

Skill reference: [`multi-mcp`](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/skills/multi-mcp/SKILL.md).
