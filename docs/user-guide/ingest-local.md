# CSV / Excel on server disk

Use this when the file already lives (or you can put it) on the same host that runs the MCP server — the common case for **local stdio** setups, since the server host is your own machine.

## CSV

Wide table: a datetime column plus pollutant columns. Skip metadata columns (battery, lat, …) with the optional `columns` parameter.

1. `load_series_from_csv` — path on the **server** disk. Handles both ISO and EU day-first dates (e.g. `23/06/2026 00:00h`).
2. `prepare_series_for_openair` — set `series_name` when the file has multiple pollutants; pass `timezone` / `timezone_name` for local exports.
3. A plot tool — `time_plot`, `calendar_plot`, …

Walkthrough: [csv-calendar-plot.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/csv-calendar-plot.md).

## Excel

Same pipeline, `load_series_from_excel` instead — `.xlsx` on **server disk only**. Handles Spanish-style `Fecha/hora` columns and duplicate-hour dedupe (common in DST-affected regional exports).

Walkthrough: [local-excel-spain.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/local-excel-spain.md).

!!! note "No bundled sample files"
    Paths like `data/felisa.xlsx` in examples are illustrative, not shipped. For a smoke test without hunting for your own Excel file, use the [committed fixture](../getting-started/quickstart.md) instead.

## Remote MCP — file lives on your PC, not the server

If the server runs elsewhere, a path on your laptop is invisible to `load_series_from_*`. See [Local file + remote MCP](ingest-local-export.md) for the right pattern.
