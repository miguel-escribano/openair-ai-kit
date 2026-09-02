# Public networks (AURN / EU)

No local file needed — the server fetches data directly from the network on the R side.

1. `import_aurn` (UK Automatic Urban and Rural Network), `import_europe` (European monitoring networks, data until Feb 2024), or `import_ukaq` (UK Air Pollution Networks — AQE, SAQN, WAQN, NI, local)
2. `prepare_series_for_openair`
3. A plot tool

In chat:

> Import MY1 NO2 for Jan-Mar 2023 and time plot it

Walkthrough: [aurn-time-plot.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/aurn-time-plot.md).

## Site metadata

Not sure of a site code? `import_meta` returns codes, names, coordinates, and available pollutants for a network.

## Requires internet

These tools need the **server host** to reach the network — relevant if your server runs somewhere with restricted outbound access.

## Local CSV exports of network data

If you already downloaded an AURN hourly CSV or CERC ADMS files rather than importing live, use `import_aurn_csv` or `import_adms` instead — same downstream pipeline (`prepare_series_for_openair` → plot), reading from **server disk**.
