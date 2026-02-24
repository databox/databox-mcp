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

Databox MCP exposes 15 tools for interacting with your data:

### Account Management

#### `list_accounts`

List all Databox accounts accessible to the authenticated user.

_No parameters._

---

### Data Sources

#### `list_data_sources`

List all data sources for a specific account.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `account_id` | string | Yes | Unique identifier of the account |

#### `create_data_source`

Create a new data source container for organizing datasets.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `name` | string | Yes | Human-readable name for the data source |
| `account_id` | string | No | Target account ID. Defaults to the account associated with the API key |

#### `delete_data_source`

Permanently remove a data source and all its associated datasets. Cannot be undone.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `data_source_id` | string | Yes | Unique identifier of the data source to delete |

#### `list_data_source_datasets`

List all datasets belonging to a specific data source.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `data_source_id` | string | Yes | Unique identifier of the data source |

---

### Datasets

#### `create_dataset`

Create a new dataset within a data source, with an optional schema.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `data_source_id` | string | Yes | ID of the parent data source |
| `name` | string | Yes | Human-readable name for the dataset |
| `columns` | string (JSON) | No | Column schema as a JSON array. Each column has `name` (string) and `data_type` (`"string"`, `"number"`, or `"datetime"`) |
| `primary_keys` | string (JSON) | No | JSON array of column names to use as composite key (e.g. `'["id"]'`) |

#### `ingest_data`

Push data records into an existing dataset.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `dataset_id` | string | Yes | Unique identifier of the target dataset (UUID) |
| `data` | string (JSON) | Yes | JSON array of records, each an object with column names as keys |

#### `get_dataset_ingestions`

Get ingestion history for a specific dataset.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `dataset_id` | string | Yes | Unique identifier of the dataset (UUID) |

#### `get_ingestion`

Get detailed information for a specific ingestion event, including record counts and dataset metrics.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `dataset_id` | string | Yes | Unique identifier of the dataset (UUID) |
| `ingestion_id` | string | Yes | Unique identifier of the ingestion event (UUID) |

#### `delete_dataset`

Permanently remove a dataset and all its data. Cannot be undone.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `dataset_id` | string | Yes | Unique identifier of the dataset to delete (UUID) |

#### `list_merged_datasets`

List all merged datasets for a specific account. Merged datasets combine data from multiple sources.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `account_id` | string | Yes | Unique identifier of the account |

---

### Metrics

#### `list_metrics`

List all metrics available for a data source (Google Analytics, Stripe, etc.).

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `data_source_id` | integer | Yes | Data source ID to list metrics for |

#### `load_metric_data`

Load data for a metric over a date range with optional dimensions and time-series granulation.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `data_source_id` | integer | Yes | Data source ID for the metric |
| `metric_key` | string | Yes | Short metric key (e.g. `"GoogleAnalytics4@sessions"`) |
| `start_date` | string | Yes | Start date in `YYYY-MM-DD` format |
| `end_date` | string | Yes | End date in `YYYY-MM-DD` format |
| `dimension` | string | No | Dimension key to break down by (e.g. `"source"`) |
| `granulation_time_unit` | integer | No | Time unit for time series: `1`=hour, `2`=day, `3`=week, `4`=month |
| `is_whole_range` | boolean | No | If `true` (default), returns single aggregated value. Automatically set to `false` when `granulation_time_unit` is provided |
| `record_limit` | integer | No | Maximum number of dimension value records to return |

---

### AI-Powered Analysis

#### `ask_genie`

Query your data using natural language, powered by Genie AI. Genie executes actual queries against your data and returns calculated results, not LLM approximations. Supports conversation threading for follow-up questions.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `dataset_id` | string | Yes | Unique identifier of the dataset to analyze (UUID) |
| `question` | string | Yes | Natural language question about the data |
| `thread_id` | string | No | Thread ID from a previous response to continue the conversation |

---

### Utilities

#### `get_current_datetime`

Get the current date and time. Use this to resolve relative date expressions like "last month" or "yesterday" before calling other tools.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `timezone` | string | No | Timezone name (e.g. `"UTC"`, `"America/New_York"`). Defaults to UTC |

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
