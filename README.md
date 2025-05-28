# MCP Server

A server implementation for Claude Desktop using the MCP SDK.

## System Requirements

- Python 3.10 or higher
- MCP SDK 1.2.0 or higher
- uv package manager

## Getting Started

### Installing uv Package Manager

#### On MacOS/Linux:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```
Make sure to restart your terminal afterwards to ensure that the uv command gets picked up.

### Project Setup

1. initialize the project:
```bash
# Create virtual environment and activate it
uv venv
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate

# Install dependencies
uv add "mcp[cli]" httpx python-dotenv beautifulsoup4
```

2. Configure environment variables:
```bash
# Create a .env file
touch .env

# Add your Serper API key
echo "SERPER_API_KEY=your_api_key_here" >> .env
```

You can get a Serper API key by signing up at [serper.dev](https://serper.dev).

### Running the Server

Start the MCP server:
```bash
uv run main.py
```
The server will start and be ready to accept connections.

## Connecting to Claude Desktop

1. Install Claude Desktop from the official website

2. Configure Claude Desktop to use your MCP server:
   Edit `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
    "mcpServers": {
        "mcp-server": {
            "command": "uv",  # It's better to use the absolute path to the uv command
            "args": [
                "--directory",
                "/ABSOLUTE/PATH/TO/YOUR/mcp-server",
                "run",
                "main.py"
            ]
        }
    }
}
```

3. Restart Claude Desktop

## Troubleshooting

If your server isn't being picked up by Claude Desktop:

- Check the configuration file path and permissions
- Verify the absolute path in the configuration is correct
- Ensure uv is properly installed and accessible
- Check Claude Desktop logs for any error messages
- Verify that your `.env` file exists and contains the required `SERPER_API_KEY`

