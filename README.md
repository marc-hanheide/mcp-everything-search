# Everything Search MCP Server

An MCP server that provides fast file searching capabilities using the Everything SDK.

## Tools

### search

Search for files and folders using Everything SDK.

Parameters:
- `query` (required): Search query string
- `max_results` (optional): Maximum number of results to return (default: 100, max: 1000)

Example:
```json
{
  "query": "*.py",
  "max_results": 50
}
```

Response includes:
- File/folder path
- File size in bytes
- Last modified date

## Prerequisites

1. Windows operating system (required - this server only works on Windows)
2. [Everything](https://www.voidtools.com/) search utility:
   - Download and install from https://www.voidtools.com/
   - **Make sure the Everything service is running**
3. Everything SDK:
   - Download from https://www.voidtools.com/support/everything/sdk/
   - Extract the SDK files to a location on your system

## Installation

### Using uv (recommended)

When using [`uv`](https://docs.astral.sh/uv/) no specific installation is needed. We will
use [`uvx`](https://docs.astral.sh/uv/guides/tools/) to directly run *mcp-server-everything-search*.

### Using PIP

Alternatively you can install `mcp-server-everything-search` via pip:

```
pip install mcp-server-everything-search
```

After installation, you can run it as a script using:

```
python -m mcp_server_everything_search
```

## Configuration

The server requires the Everything SDK DLL to be available:

Environment variable:
   ```
   EVERYTHING_SDK_PATH=path\to\Everything-SDK\dll\Everything64.dll
   ```

### Usage with Claude Desktop

Add this to your `claude_desktop_config.json`:

<details>
<summary>Using uvx</summary>

```json
"mcpServers": {
  "everything-search": {
    "command": "uvx",
    "args": ["mcp-server-everything-search"],
    "env": {
      "EVERYTHING_SDK_PATH": "path/to/Everything-SDK/dll/Everything64.dll"
    }
  }
}
```
</details>

<details>
<summary>Using pip installation</summary>

```json
"mcpServers": {
  "everything-search": {
    "command": "python",
    "args": ["-m", "mcp_server_everything_search"],
    "env": {
      "EVERYTHING_SDK_PATH": "path/to/Everything-SDK/dll/Everything64.dll"
    }
  }
}
```
</details>

## Debugging

You can use the MCP inspector to debug the server. For uvx installations:

```
npx @modelcontextprotocol/inspector uvx mcp-server-everything-search
```

Or if you've installed the package in a specific directory or are developing on it:

```
git clone https://github.com/mamertofabian/mcp-everything-search.git
cd mcp-everything-search/src/mcp_server_everything_search
npx @modelcontextprotocol/inspector uv run mcp-server-everything-search
```

Using PowerShell, running `Get-Content -Path "$env:APPDATA\Claude\logs\mcp*.log" -Tail 20 -Wait` will show the logs from the server and may help you debug any issues.

## Development

If you are doing local development, there are two ways to test your changes:

1. Run the MCP inspector to test your changes. See [Debugging](#debugging) for run instructions.

2. Test using the Claude desktop app. Add the following to your `claude_desktop_config.json`:

```json
"everything-search": {
  "command": "uv",
  "args": [
    "--directory",
    "/path/to/mcp-everything-search/src/mcp_server_everything_search",
    "run",
    "mcp-server-everything-search"
  ],
  "env": {
    "EVERYTHING_SDK_PATH": "path/to/Everything-SDK/dll/Everything64.dll"
  }
}
```

## License

This MCP server is licensed under the MIT License. This means you are free to use, modify, and distribute the software, subject to the terms and conditions of the MIT License. For more details, please see the LICENSE file in the project repository.

## Disclaimer

This project is not affiliated with, endorsed by, or sponsored by voidtools (the creators of Everything search utility). This is an independent project that utilizes the publicly available Everything SDK. 
