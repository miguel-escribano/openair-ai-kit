# Testing tiers

Three tiers, each in a different repo, each answering a different question.

| Tier | Where | Purpose |
|------|-------|---------|
| **Unit** | server repo, `pytest` | Ingest, prepare, encoding, DST — fast, mostly no R required |
| **Host smoke** | server repo, `python check_integrations.py` | Tool registration + R subprocess when R is installed |
| **Acceptance** | client plugin repo, `tests/` | 12+4 plots against a **deployed** MCP server — legends, encoding, end-to-end |

Run all three before proposing (or trusting) a release.

## Unit tests

```bash
cd openair-3-mcp-server-oss
pytest
```

Covers ingest, `prepare_series_for_openair`, text encoding, and DST edge cases. Fast, and mostly doesn't need R installed.

## Host smoke

```bash
python check_integrations.py
```

Confirms tool registration succeeds and (when R is available) that the R subprocess bridge works. Optional live network smoke: `OPENAIR_SMOKE_NETWORK=1 python check_integrations.py`.

## Acceptance harness

This is the **authoritative** check — it proves a deployed MCP server actually produces correct plots, not just that the code imports.

```bash
cd openair-3-mcp-client-plugin-oss
export OPENAIR_MCP_TOKEN=…
python tests/run_series_exercises.py    # 12 checks → tests/output/series/
python tests/run_wind_exercises.py      # 4 checks → tests/output/wind/
```

PowerShell:

```powershell
$env:OPENAIR_MCP_TOKEN = "…"
python tests/run_series_exercises.py
python tests/run_wind_exercises.py
```

**Pass criteria:** 12/12 + 4/4. Visual check: `tests/output/series/02_time_plot_all.png` should show correctly-encoded legends (NO₂ / PM₁₀ / O₃, not mojibake); `12_summary_plot_all.png` should show completeness bars.

It runs against the **Felisa fixture** (`tests/fixtures/felisa_munarriz.json`) — real pollutant readings plus Open-Meteo ERA5 wind for a Pamplona station, 2026-05-31 to 2026-06-28 UTC. Not run in CI by default — it needs R on the server host and a live token.

## VS Code Copilot smoke

Same fixture, chat-driven instead of scripted — see [vscode-chat-felisa.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/examples/vscode-chat-felisa.md). Useful when you want to eyeball the chat experience, not just the harness output.

Full checklist: [server repo docs/VALIDATION.md](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/docs/VALIDATION.md).
