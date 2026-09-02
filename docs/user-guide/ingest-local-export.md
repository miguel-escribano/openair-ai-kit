# Local file + remote MCP

Your MCP server runs on another host, but your CSV/Excel file is on your own machine. `load_series_from_csv` / `load_series_from_excel` only see the **server's** disk — so a client-side bridge is needed.

## Preferred: `export_local_series.py`

Run this on **your** machine (`pip install -e .` from the [server repo](https://github.com/miguel-escribano/openair-3-mcp-server-oss) — no R required for this step):

```bash
python scripts/export_local_series.py --file /path/on/your/pc/data.xlsx ...
```

It reads your local file and produces `SeriesV1` JSON. Hand that JSON to `prepare_series_for_openair(data=…)` on the remote MCP — the agent reads the export and calls the remote tool; it never re-parses or reshapes the data itself.

See the client plugin's [`ingest-local-export` skill](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/skills/ingest-local-export/SKILL.md) for the exact invocation.

## Alternatives, in order of preference

1. **Copy the file to server disk**, then use [CSV / Excel on server disk](ingest-local.md) normally.
2. **Switch to local stdio** — if you can run the server on your own machine instead, the file is no longer "remote" at all.
3. **`load_series_from_upload`** — last resort. Base64-encodes the file into the MCP call; default limit 1 MB raw, configurable server-side via `OPENAIR_INGEST_MAX_BYTES`. Fine for a quick sample, not for a full export.

See the client plugin's [`ingest-local` skill](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/skills/ingest-local/SKILL.md) for the upload path.

## Why not just paste the data into chat?

The agent should never hand-build a `SeriesV1` array from pasted numbers — date parsing, timezone handling, and gap alignment are exactly the steps this kit keeps deterministic and off the model. See [Concepts → Why not build the array in chat?](../getting-started/concepts.md#why-not-build-the-array-in-chat).
