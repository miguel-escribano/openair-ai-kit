# Installation

The kit is two repos: the **server** (Python + R, runs the openair tools) and the **client plugin** (wires your IDE/agent to that server). Install the server first.

## Choose your setup

| | **A — Local stdio** | **B — Local HTTP** | **C — Remote HTTP** |
|---|---|---|---|
| **R location** | Same machine as the IDE | Same machine as the IDE | Another host (VM, cloud, lab server) |
| **You need** | R + openair + Python venv on the same machine as the IDE | Same machine, server on port 8001 | R on another host, Node.js on the IDE machine |
| **Client MCP** | Spawn `python … --transport stdio` (no Node) | `mcp-remote` → `http://127.0.0.1:8001/sse` | `mcp-remote` → your HTTPS URL (+ token if enabled) |

Path A avoids Node.js and a separate HTTP process entirely — simplest if your IDE and R already live on the same machine. Paths B and C both go through `mcp-remote`; C just points it at a remote URL instead of localhost.

## 1. Run the server

```bash
git clone https://github.com/miguel-escribano/openair-3-mcp-server-oss
cd openair-3-mcp-server-oss
python -m venv .venv
# Windows: .venv\Scripts\activate
# Unix: source .venv/bin/activate
pip install -e .
cp .env.example .env
python check_integrations.py
```

Install R packages on the **same machine** as the server:

```r
install.packages(c("openair", "jsonlite"), repos = "https://cloud.r-project.org")
# optional: legendry only adds the cor_plot dendrogram — everything else works without it
install.packages("legendry", repos = "https://cloud.r-project.org")
```

Run it — HTTP (paths B/C):

```bash
fastmcp run server.py:mcp --transport http --port 8001
```

...or stdio (path A — IDE and R on the same machine):

```bash
fastmcp run server.py:mcp --transport stdio
```

R 4.1+ with **openair 3.x** (ggplot2 backend) is required on the server host. Run `health_r` (an MCP tool) after install to confirm.

## 2. Install the client plugin

```bash
git clone https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss
cd openair-3-mcp-client-plugin-oss
cp .mcp.json.example .mcp.json   # gitignored — edit for your path (A/B/C)
```

**Path A (local stdio)**:

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

Windows: use `.venv\\Scripts\\python.exe`.

**Paths B/C (HTTP + mcp-remote)** — requires Node.js 18+ on the IDE machine:

```json
{
  "mcpServers": {
    "openair-3-mcp": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "http://127.0.0.1:8001/sse",
        "--header",
        "X-MCP-Token: YOUR_MCP_TOKEN"
      ]
    }
  }
}
```

Local: `http://127.0.0.1:8001/sse`, drop `--header ...` if you have no token auth. Remote: swap in your server URL and keep the token header if your proxy requires it.

**VS Code:** use the same JSON under `.vscode/mcp.json` with a top-level `"servers"` key instead of `"mcpServers"`.

## 3. Install the plugin in your IDE

- **Claude Code:** `claude plugin install /path/to/openair-3-mcp-client-plugin-oss`
- **Cursor / Codex / VS Code:** open the plugin folder or add it to your plugin path; skills live under `skills/`.

Restart the IDE session after any MCP config change.

## Next

[Quickstart →](quickstart.md) — a first working example that needs no data of your own.
