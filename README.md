# Databox MCP Server

**Chat with your data. Anywhere.**

The Databox MCP (Model Context Protocol) server enables you to interact with your Databox metrics and data directly through AI assistants and other MCP-compatible applications. Query your business metrics, analyze trends, and get insights from your data using natural language.

## 🌟 Features

- **Natural Language Queries**: Ask questions about your data in plain English
- **Real-time Data Access**: Connect directly to your Databox metrics and KPIs
- **Multi-Source Integration**: Access data from all your connected data sources
- **AI-Powered Insights**: Leverage AI to analyze trends and patterns in your data
- **Secure Authentication**: OAuth-based secure access to your Databox account

## 📚 Resources

- **Learn More**: [Databox MCP Overview](https://databox.com/mcp)
- **Blog Post**: [Chat with your data anywhere](https://databox.substack.com/p/databox-mcp-chat-with-your-data-anywhere)
- **Documentation**: [MCP Developer Guide](https://developers.databox.com/docs/mcp/overview)

## 🚀 Getting Started

### Prerequisites

- Node.js 18 or higher
- A Databox account with an active subscription
- MCP-compatible client (e.g., Claude Desktop, Continue, or other MCP clients)

### Installation

#### Option 1: Using npx (Recommended)

You can run the Databox MCP server directly using npx without installation:

```bash
npx @databox/mcp-server
```

#### Option 2: Global Installation

Install the server globally:

```bash
npm install -g @databox/mcp-server
```

Then run:

```bash
databox-mcp
```

#### Option 3: Local Installation

Install as a dependency in your project:

```bash
npm install @databox/mcp-server
```

### Configuration

#### Claude Desktop

Add the following to your Claude Desktop configuration file:

**macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
**Windows**: `%APPDATA%\Claude\claude_desktop_config.json`

```json
{
  "mcpServers": {
    "databox": {
      "command": "npx",
      "args": ["-y", "@databox/mcp-server"]
    }
  }
}
```

#### Other MCP Clients

Refer to your MCP client's documentation for configuration instructions. The server implements the standard MCP protocol and should work with any compatible client.

## 🔧 Usage

Once configured, you can interact with your Databox data through your MCP client. Here are some example queries:

- "What are my top performing metrics this week?"
- "Show me the trend for website traffic over the last 30 days"
- "Compare my sales data from this month vs last month"
- "What's my current conversion rate?"
- "Summarize my marketing KPIs"

## 🔐 Authentication

The server uses OAuth to securely connect to your Databox account. On first use, you'll be prompted to authenticate and grant the necessary permissions.

## 🛠️ Development

### Building from Source

```bash
# Clone the repository
git clone https://github.com/databox/databox-mcp.git
cd databox-mcp

# Install dependencies
npm install

# Build the project
npm run build

# Run the server
npm start
```

### Running Tests

```bash
npm test
```

## 📖 API & Tools

The Databox MCP server provides the following tools:

- **query_metrics**: Query specific metrics from your Databox account
- **list_databoards**: List all available databoards
- **get_databoard**: Get details and data from a specific databoard
- **analyze_trend**: Analyze trends in your metrics over time
- **compare_periods**: Compare metrics across different time periods

## 🤝 Support

- **Documentation**: Visit [developers.databox.com/docs/mcp](https://developers.databox.com/docs/mcp/overview)
- **Issues**: Report issues on [GitHub Issues](https://github.com/databox/databox-mcp/issues)
- **Community**: Join discussions on [Databox Community](https://databox.com/community)

## 📄 License

See [LICENSE](LICENSE) file for details.

## 🔗 Related Projects

- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Databox API](https://developers.databox.com/)
- [Databox Platform](https://databox.com/)

---

Made with ❤️ by [Databox](https://databox.com)
