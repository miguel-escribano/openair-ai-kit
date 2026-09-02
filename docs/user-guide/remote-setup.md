# Transports — stdio / HTTP / remote

Pick a transport based on where your IDE runs relative to R. See also [Getting started → Installation](../getting-started/installation.md) for the setup steps.

## stdio — same machine

IDE spawns the Python server process directly. No HTTP port, no Node.js, no `mcp-remote`.

```bash
fastmcp run server.py:mcp --transport stdio
```

Client `.mcp.json`:

```json
{
  "mcpServers": {
    "openair-3-mcp": {
      "command": "/path/to/openair-3-mcp-server-oss/.venv/bin/python",
      "args": ["-m", "fastmcp", "run", "server.py:mcp", "--transport", "stdio"],
      "cwd": "/path/to/openair-3-mcp-server-oss"
    }
  }
}
```

Windows: `.venv\\Scripts\\python.exe`.

## HTTP — local or remote

Server runs as its own process, reachable over HTTP. Works whether that's `127.0.0.1` on your own machine or a remote host.

```bash
fastmcp run server.py:mcp --transport http --port 8001
```

Client connects via `mcp-remote` (needs Node.js 18+ on the IDE machine):

```json
{
  "mcpServers": {
    "openair-3-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://your-host/openair-3-mcp-server-oss/sse",
        "--header",
        "X-MCP-Token: YOUR_MCP_TOKEN"
      ]
    }
  }
}
```

Local: use `http://127.0.0.1:8001/sse` and drop `--header ...` if you haven't enabled token auth. Remote: use your server's HTTPS URL and keep the token header if your proxy requires it — never commit a real token, `.mcp.json` should stay gitignored.

## VS Code

Same JSON, under `.vscode/mcp.json`, with a top-level `"servers"` key instead of `"mcpServers"` (same `command` / `args` per server).

## Server-side configuration

Copy `.env.example` → `.env` on the server host:

| Variable | Purpose |
|----------|---------|
| `RSCRIPT_PATH` | Path to `Rscript` (default `Rscript`) |
| `RSCRIPT_TIMEOUT_SEC` | Default R subprocess timeout |
| `OPENAIR_ARTIFACTS_DIR` | Where PNGs are written (default `artifacts/`) |
| `OPENAIR_MCP_TRANSPORT` | `http` or `stdio` when using `python server.py` |
| `OPENAIR_MCP_PORT` | HTTP port (default `8001`) |

R only needs to run on the **server** — never on every IDE client.

## Remote MCP — path caveat

`load_series_from_excel(path="data/felisa.xlsx")` only works if that file exists on the **server host**. Example paths in docs and chat prompts are illustrative, not bundled. For remote setups with a local file, see [Local file + remote MCP](ingest-local-export.md).
