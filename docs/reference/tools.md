# Tool catalog

45 tools total — 37 R-backed (plots, imports, stats) plus 8 Python pipeline tools. Plot tools return `[text, image]` MCP blocks so clients show the chart inline; stats tools return structured JSON. Full descriptions live in the [server README](https://github.com/miguel-escribano/openair-3-mcp-server-oss#available-tools) — condensed by category here.

## Pipeline (Python)

| Tool | Purpose |
|------|---------|
| `load_series_from_csv` | Wide CSV on server disk → `SeriesV1` |
| `load_series_from_excel` | `.xlsx` on server disk → `SeriesV1` |
| `load_series_from_upload` | Base64 CSV/xlsx upload → `SeriesV1` (default 1 MB limit) |
| `prepare_series_for_openair` | Align timestamps, granularity, timezone; merges `json_exports` from other MCPs |
| `ping` | Server liveness |
| `health_r` | R + openair install/version check |
| `openair_docs` | Index of openair functions exposed as tools |
| `openair_function_help` | R help text for a named openair function |

## Data import (R)

| Tool | Purpose |
|------|---------|
| `import_aurn` | UK AURN network (internet required) |
| `import_adms` | CERC ADMS files on server disk |
| `import_aurn_csv` | UK AURN hourly CSV export on server disk |
| `import_ukaq` | UK Air Pollution Networks (AQE, SAQN, WAQN, NI, local) |
| `import_europe` | European monitoring networks (data until Feb 2024) |
| `import_meta` | Site metadata — codes, names, coordinates, pollutants |
| `import_traj` | Pre-calculated HYSPLIT 96-hour back trajectories |

## Time series plots (R)

`time_plot`, `summary_plot`, `calendar_plot`, `time_variation`, `variation_plot`, `time_prop`, `trend_level`, `smooth_trend`, `theil_sen`, `scatter_plot`, `cor_plot`, `conditional_quantile`, `taylor_diagram`.

## Polar / wind (R)

Requires `ws` / `wd` in prepared data: `polar_plot`, `polar_annulus`, `polar_diff`, `polar_freq`, `polar_cluster`, `pollution_rose`, `percentile_rose`, `wind_rose`.

## Trajectory (R)

`traj_plot`, `traj_level`, `traj_cluster`.

## Stats & transforms (R)

`aq_stats`, `mod_stats`, `calc_percentile`, `time_average`, `rolling_mean`, `rolling_quantile`.

## Adding a tool

Tools are auto-discovered from `r/scripts/*.R` manifest headers at server startup — no Python change required. See [server CONTRIBUTING.md](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/CONTRIBUTING.md#adding-a-tool).

!!! note "Prerequisite"
    R 4.1+ with **openair 3.x** (ggplot2 backend) on the server host. Run `health_r` after install.
