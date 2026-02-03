# Databox MCP

**Chat with your data. Anywhere.**

Databox MCP is a [Model Context Protocol](https://modelcontextprotocol.io/) server that connects your business data to AI assistants. Ask questions about your metrics in plain English—no SQL, no dashboard building, no data exports.

[![Databox](https://img.shields.io/badge/Databox-MCP-blue)](https://databox.com/mcp)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-green)](https://modelcontextprotocol.io/)

## Overview

Databox MCP enables AI tools like Claude, Cursor, n8n, and Gemini CLI to access and analyze your Databox data conversationally. It transforms how you interact with business metrics—instead of navigating dashboards, you simply ask questions and get instant answers.

**Key Benefits:**
- Query your data using natural language
- Works with 130+ existing Databox integrations
- No additional cost for Databox users
- Setup in under 60 seconds

## Supported AI Clients

| Client | Status |
|--------|--------|
| Claude Desktop | Supported |
| Claude Web | Supported |
| Cursor | Supported |
| n8n | Supported |
| Gemini CLI | Supported |
| Any MCP-compatible tool | Supported |

## Quick Setup

### Claude Desktop

Add to your `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "databox": {
      "type": "http",
      "url": "https://mcp.databox.com/mcp"
    }
  }
}
```

### Claude Web / Claude Desktop App

1. Go to **Settings** → **Connectors**
2. Click **Add Custom Connector**
3. Enter the remote server URL: `https://mcp.databox.com/mcp`
4. Complete the authorization flow

### Cursor

Add the Databox MCP server in Cursor's MCP settings with the URL `https://mcp.databox.com/mcp`.

### n8n

Use an **HTTP Request** node pointing to `https://mcp.databox.com/mcp` and build your workflows from there.

## Available Tools

Databox MCP exposes 16 tools for interacting with your data:

### Account Management
- **list_accounts** – List all Databox accounts you have access to

### Data Sources
- **list_data_sources** – List data sources for an account
- **create_data_source** – Create a new data source
- **delete_data_source** – Remove a data source
- **list_data_source_datasets** – List datasets within a data source

### Datasets
- **create_dataset** – Create a new dataset with schema definition
- **delete_dataset** – Remove a dataset
- **ingest_data** – Push data records into a dataset
- **get_ingestion** – Check ingestion status and metrics
- **get_ingestions** – List all ingestions for a dataset

### Metrics
- **list_metrics** – List all metrics available for a data source (Google Analytics, Stripe, etc.)
- **load_metric_data** – Load metric data over a date range with optional dimensions and time-series granulation

### AI-Powered Analysis
- **ask_genie** – Query your data using natural language (powered by Genie AI)
  - Supports conversation threading for follow-up questions
  - Translates business questions into precise queries
  - Returns calculated results, not LLM approximations

### Utilities
- **get_current_datetime** – Get current date/time for resolving relative date expressions

## How It Works

Databox MCP uses a three-layer architecture to ensure accurate, reliable answers:

1. **Data Platform** – Structured datasets with schemas, types, and validation
2. **Analytic Query Engine** – Executes actual queries (aggregations, joins, filters)
3. **Semantic Layer** – Understands business definitions and metric relationships

The AI never touches your calculations directly. It formulates queries, the engine executes them, and the AI summarizes the results. This means you get real calculations, not statistical approximations.

## Authentication

Databox MCP uses secure authentication:

- **OAuth 2.0** for user authorization
- **JWT token validation** for secure sessions
- **API key authentication** for programmatic access

Your data remains within your Databox account with existing governance standards. AI access is limited to explicitly granted data permissions.

## Security

- Encrypted connections (HTTPS)
- Scope-based authorization
- Audit trails and ingestion history
- No vendor lock-in (universal MCP standard)
- Data isolation per account

## Use Cases

**Ad-hoc Analysis**
> "What was our conversion rate last week compared to the previous week?"

**Cross-source Insights**
> "Calculate ROAS by combining ad spend from Google Ads with revenue from Stripe"

**Trend Detection**
> "Which product category has the highest refund rate this quarter?"

**Automated Alerts**
> "Alert me if the 3-day conversion rate drops below 2%"

**Data Cleanup**
> Push messy CSV exports and let Databox normalize dates, formats, and schemas automatically

**Direct Metric Queries**
> "Show me Google Analytics sessions for the last 30 days broken down by traffic source"

**Time-Series Analysis**
> "Load daily page views for January with weekly aggregation"

**Dimension Breakdowns**
> "What are the top 10 countries by revenue from Stripe?"

## Resources

- [Databox MCP Landing Page](https://databox.com/mcp)
- [Blog: Chat with Your Data Anywhere](https://databox.substack.com/p/databox-mcp-chat-with-your-data-anywhere)
- [Model Context Protocol Specification](https://modelcontextprotocol.io/)
- [Databox Help Center](https://help.databox.com/)

## Support

For questions and support:
- Visit the [Databox Help Center](https://help.databox.com/)
- Contact [support@databox.com](mailto:support@databox.com)

---

Built by [Databox](https://databox.com) — Track all your business metrics in one place.
