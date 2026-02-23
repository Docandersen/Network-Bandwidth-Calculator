# Network-Bandwidth-Calculator
# Bandwidth Calculator MCP

A fully functional **Model Context Protocol (MCP) server** that connects AI assistants to routers, AIOps solutions, and network management platforms to calculate comprehensive bandwidth requirements.

## Quick Start

```bash
pip install -r requirements.txt
python bandwidth_mcp.py          # stdio mode (Claude Desktop)
python bandwidth_mcp.py --http   # HTTP mode (port 8000)
```

## Claude Desktop Config

```json
{
  "mcpServers": {
    "bandwidth-calculator": {
      "command": "python",
      "args": ["/path/to/bandwidth_mcp.py"],
      "env": { "SNMP_COMMUNITY": "your-community-string" }
    }
  }
}
```

## 13 MCP Tools

| Tool | Purpose |
|---|---|
| `bw_add_connector` | Register a router, SD-WAN controller, or AIOps platform |
| `bw_list_connectors` | List all sources with health status |
| `bw_get_device_bandwidth` | Per-device/interface utilization metrics |
| `bw_get_network_summary` | Network-wide aggregate + top busiest links |
| `bw_calculate_requirements` | Bandwidth requirements (peak/P95/avg/forecast models) |
| `bw_compare_historical_trends` | Growth rates, trend direction, days to critical |
| `bw_predict_bandwidth_demand` | ML demand forecasting (linear/exponential/seasonal) |
| `bw_check_capacity_headroom` | RAG status against SLA threshold profiles |
| `bw_get_application_traffic` | Per-app bandwidth breakdown (DPI/NetFlow) |
| `bw_get_anomaly_alerts` | Active anomalies from AIOps platforms |
| `bw_correlate_events` | Anomaly ↔ change event root cause correlation |
| `bw_run_audit` | Full audit with progress reporting + recommendations |
| `bw_generate_report` | Capacity planning report (Markdown / JSON / CSV) |

## Supported Connector Types

**Network Devices**: snmp, netconf, gnmi, rest_api  
**SD-WAN**: meraki, viptela, velocloud  
**AIOps/NMS**: thousandeyes, solarwinds, dynatrace, prtg, bigpanda, moogsoft

## Calculation Models

- `peak_utilization` — max observed + headroom  
- `95th_percentile` — P95 of 5-min samples + headroom *(recommended)*  
- `average_plus_headroom` — mean + headroom  
- `aiops_forecast` — ML-weighted forward projection  

## SLA Profiles

`default` (70/85/95%), `enterprise-standard` (65/80/90%), `isp-core` (50/70/85%), `datacenter-wan` (60/75/88%)

## Demo Mode

Ships with 14 pre-seeded connectors (NYC, LAX, CHI, LON, FRA) with realistic traffic simulation. Use `bw_add_connector` to register real devices.

## Environment Variables

| Variable | Default | Description |
|---|---|---|
| `SNMP_COMMUNITY` | `public` | SNMP community string |
| `MCP_TRANSPORT` | `stdio` | `stdio` or `streamable_http` |
| `MCP_PORT` | `8000` | HTTP port |
