# silicon-index-backend-api

Backend API for Silicon Index. Currently: an MCP (Model Context Protocol) server
exposing market/pricing data to AI agents.

## MCP server

See [`src/modules/mcp/README.md`](./src/modules/mcp/README.md) for the tool list and
architecture notes.

```bash
bun install

# Run locally (Bun, port 8080 by default)
npm run mcp:serve

# Or against Cloudflare Workers dev
npm run mcp:dev
```

Health check: `GET /health`. MCP Streamable HTTP transport is mounted at `/`
(`POST`/`GET`/`DELETE`), implemented with `@modelcontextprotocol/server`.

Deploy to Cloudflare Workers: `npm run mcp:deploy` (see `deploy/mcp/wrangler.toml`), or
build the Docker image: `docker build -f deploy/mcp/Dockerfile -t silicon-index-mcp-api .`
(build context must be the repo root).

Read-only, public data — same trust posture as the market-database module, so the
server requires no auth token to call.
