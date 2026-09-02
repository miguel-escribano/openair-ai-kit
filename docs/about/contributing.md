# Contributing

This landing/docs repo doesn't hold code — contributions go to whichever half of the binomio they touch.

| Change is about... | Go to |
|---|---|
| A tool, R script, ingest logic, contracts, server config | [openair-3-mcp-server-oss](https://github.com/miguel-escribano/openair-3-mcp-server-oss) — [CONTRIBUTING.md](https://github.com/miguel-escribano/openair-3-mcp-server-oss/blob/main/CONTRIBUTING.md) |
| A skill, the agent persona, examples, the acceptance harness, IDE wiring | [openair-3-mcp-client-plugin-oss](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss) — [CONTRIBUTING.md](https://github.com/miguel-escribano/openair-3-mcp-client-plugin-oss/blob/main/CONTRIBUTING.md) |
| This site's content, the landing README, cross-repo docs | Open a PR against [openair-ai-kit](https://github.com/miguel-escribano/openair-ai-kit) directly — docs live under `docs/`, built with mkdocs + Material |

## Reporting bugs

Use [GitHub issues on the server repo](https://github.com/miguel-escribano/openair-3-mcp-server-oss/issues) — it's the shared tracker for the binomio. Include the transport you're using (stdio/HTTP), R version (`health_r` output if you have it), and the tool + input shape that triggered the problem.

## Both repos, one rule

The two code repos are **versioned together** — a change that assumes a new server tool or a changed contract should flag that in the PR description, since the client plugin and server ship matching release tags.
