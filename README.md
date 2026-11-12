# GAJA (가자) - Korea Travel & Measured Visits MCP Server

[![MCP Registry](https://img.shields.io/badge/MCP-Registry-blue.svg)](https://modelcontextprotocol.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status: Live](https://img.shields.io/badge/Status-Live%20Remote%20MCP-emerald.svg)](https://gaja.mocean.kr/mcp)

GAJA is a production remote Model Context Protocol (MCP) server providing **verified travel destinations and optimized itineraries** across 250+ administrative districts in South Korea, powered by real-world telecommunication and navigation visit big data.

---

## 🌟 Key Features

- **Real-World Measured Big Data**: Uses actual mobile carrier roaming and navigation movement volumes from the Korea Tourism Organization (TourAPI) and TMAP Big Data, eliminating hallucinations.
- **Full Regional Coverage**: 250+ cities, counties, and districts across South Korea (Seoul, Gangwon, Jeju, Busan, Inje, etc.).
- **Multi-day Course Generator**: Automatically generates 1-day to 8-day structured itineraries with morning/lunch/afternoon/dinner/lodging schedules and live weather forecasts.
- **Foreign Visitor Surge Detection**: Identifies rapidly emerging travel spots popular among inbound foreign tourists by nationality.
- **Production-Ready & High Performance**: Deployed over HTTP with Streamable-HTTP (`stateless_http=True`), payload optimized under 16KB for compatibility with all MCP clients.

---

## 📡 Live Remote MCP Endpoints

| Resource | URL | Description |
|---|---|---|
| **MCP Live Endpoint** | `https://gaja.mocean.kr/mcp` | Streamable-HTTP / JSON-RPC Transport |
| **RFC Standard Discovery** | `https://gaja.mocean.kr/.well-known/mcp.json` | Discovery manifest |
| **Server Metadata** | `https://gaja.mocean.kr/.well-known/mcp-server.json` | Schema & version descriptor |
| **AI Context Index** | `https://gaja.mocean.kr/llms.txt` | Context for LLMs & AI search engines |

---

## 🛠️ Provided Tools

### 1. `gaja_recommend_trending_places`
- **Description**: Recommends top trending travel destinations in South Korea based on statistically verified mobile visit counts.
- **Parameters**:
  - `limit` (integer, optional): Maximum number of destinations to return (default: 5, max: 20).
  - `category` (string, optional): Travel category filter (`nature`, `culture`, `leisure`, `food`).

### 2. `gaja_recommend_places`
- **Description**: Generates an optimized, day-by-day travel itinerary with verified attractions, restaurants, and lodgings for any Korean district.
- **Parameters**:
  - `query` (string, required): Destination name (e.g. `인제군`, `강릉시`, `제주도`, `Inje`, `Gangneung`).
  - `days` (integer, optional): Duration in days (1 to 8, default: 2).
  - `companion` (string, optional): Travel companion type (`solo`, `couple`, `family`, `friends`).

### 3. `gaja_get_foreign_surge`
- **Description**: Analyzes regional districts experiencing a rapid surge in inbound foreign visitors compared to the previous period.
- **Parameters**:
  - `top_n` (integer, optional): Number of surging districts to return (default: 5).
  - `nationality` (string, optional): Filter by visitor nationality (e.g., `ALL`, `JP`, `CN`, `US`).

### 4. `gaja_get_data_freshness`
- **Description**: Returns the statistical baseline date, aggregation window, data provider provenance, and sample size of the underlying datasets.

---

## 🚀 Client Configuration

### Claude Desktop (`claude_desktop_config.json`)

```json
{
  "mcpServers": {
    "gaja": {
      "url": "https://gaja.mocean.kr/mcp"
    }
  }
}
```

*Note: For Claude Desktop versions supporting remote HTTP MCP, simply add the URL above.*

### Cursor / Windsurf

Add a new MCP server in settings:
- **Type**: `command` (with mcp-proxy) or direct `streamable-http` / `sse`
- **URL**: `https://gaja.mocean.kr/mcp`

### Kakao PlayMCP

GAJA is registered on Kakao PlayMCP (`gaja` identifier) with zero-authentication remote access:
- **Endpoint**: `https://gaja.mocean.kr/mcp`

---

## 📊 Data Reliability & Provenance

Every recommendation returned by GAJA includes a `PROVENANCE` verification tag linking back to official government and telecom datasets:
- **Korea Tourism Organization TourAPI 4.0**
- **TMAP Big Data Navigation Destination Index**
- **Korea Meteorological Administration Realtime Forecast**

---

## 📄 License

This MCP server metadata and client integration specifications are licensed under the [MIT License](LICENSE).
Data sources comply with public data licenses (KOGL Type 1).
