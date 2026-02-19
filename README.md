[![License: MPL 2.0](https://img.shields.io/badge/License-MPL_2.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)

# seats.aero MCP Server

**Not affiliated with seats.aero**

A TypeScript-based MCP server for searching award flight availability through the [seats.aero](https://seats.aero) API via Claude or any other MCP client.

You will need a seats.aero API key via a [seats.aero Pro membership](https://seats.aero) to use this server.

## Quick Start (Pre-built Binary)

Download the latest binary for your platform from [Releases](https://github.com/gavgrego/seats.aero-mcp-server/releases/latest):

| Platform | Binary |
|----------|--------|
| macOS (Apple Silicon) | `seats-mcp-darwin-arm64` |
| macOS (Intel) | `seats-mcp-darwin-x64` |
| Linux (x64) | `seats-mcp-linux-x64` |
| Linux (ARM64) | `seats-mcp-linux-arm64` |

After downloading, make it executable:

```bash
chmod +x seats-mcp-darwin-arm64
```

Verify the download (optional):

```bash
# Download checksums.txt from the same release, then:
sha256sum -c checksums.txt
```

## Configuration

### Claude Code

```bash
claude mcp add seats -- /path/to/seats-mcp-darwin-arm64
```

Then set your API key:

```bash
claude mcp update seats -e SEATS_API_KEY=your-api-key
```

### Claude Desktop

Add the following to your `claude_desktop_config.json`:

- macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
- Windows: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "seats": {
      "command": "/path/to/seats-mcp-darwin-arm64",
      "env": {
        "SEATS_API_KEY": "your-api-key"
      }
    }
  }
}
```

## Tools

### `get_flights`

Search for cached award flights. Supports the same parameters as the [cached search endpoint](https://developers.seats.aero/reference/cached-search) including origin/destination airports, dates, cabin class, and carriers.

### `get_bulk_avail`

Retrieve bulk availability from a specific mileage program (source). Supports the same parameters as the [bulk availability endpoint](https://developers.seats.aero/reference/get-availability).

### `get_routes`

Retrieve routes from a specific mileage program (source). Supports the same parameters as the [routes endpoint](https://developers.seats.aero/reference/get-routes-1).

## Development

### Prerequisites

- [Node.js](https://nodejs.org/) (v18+)
- [pnpm](https://pnpm.io/)
- [Bun](https://bun.sh/) (for compiling binaries)

### Setup

```bash
pnpm install
pnpm build
pnpm start
```

### Building Binaries Locally

```bash
# Build all platforms
bun run compile

# Build a specific platform
bun run compile:darwin-arm64
```

## Releasing

Releases are automated via GitHub Actions. To create a new release:

```bash
git tag v1.0.2
git push origin v1.0.2
```

This builds binaries for all platforms and publishes them as a GitHub Release with SHA-256 checksums.

## License

[MPL-2.0](LICENSE)
