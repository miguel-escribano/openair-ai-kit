# Quickstart

Two ways to get a first chart with nothing of your own to prepare: the committed test fixture, or a public network import.

## Option 1 — committed fixture (no data hunting)

The client plugin ships a real fixture — `tests/fixtures/felisa_munarriz.json` — pollutant readings plus ERA5 wind for a station in Pamplona, Spain. Useful the moment the plugin is installed, remote MCP or not.

In chat:

> Use `tests/fixtures/felisa_munarriz.json`, prepare hourly Europe/Madrid, time_plot all pollutants — MCP only

This chains: read the fixture → `prepare_series_for_openair` (aligns timestamps/timezone) → `time_plot` (renders the PNG inline).

See the full walkthrough: [vscode-chat-felisa.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/vscode-chat-felisa.md).

## Option 2 — public network import

No local files needed — pulls UK AURN data directly.

In chat:

> Import MY1 NO2 for Jan-Mar 2023 and time plot it

This chains: `import_aurn` → `prepare_series_for_openair` → `time_plot`.

See the full walkthrough: [aurn-time-plot.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/aurn-time-plot.md).

## Verify the harness end-to-end

If you want the full 16-check acceptance run rather than one chat prompt:

```powershell
$env:OPENAIR_MCP_TOKEN = "…"
python tests/run_series_exercises.py    # 12 checks → tests/output/series/
python tests/run_wind_exercises.py      # 4 checks → tests/output/wind/
```

Pass criteria: 12/12 + 4/4. Details: [Reference → Testing tiers](../reference/testing.md).

## Your own data next

Once one of the above works, move to your own CSV/Excel or another data modality — see the [User guide](../user-guide/ingest-local.md) for the path that matches where your data lives.
