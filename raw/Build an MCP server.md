---
title: "Build an MCP server"
source: "https://modelcontextprotocol.io/docs/develop/build-server"
author:
published:
created: 2026-05-10
description: "Get started building your own server to use in Claude for Desktop and other clients."
tags:
  - "clippings"
---
In this tutorial, we’ll build a simple MCP weather server and connect it to a host, Claude for Desktop.

### What we’ll be building

We’ll build a server that exposes two tools: `get_alerts` and `get_forecast`. Then we’ll connect the server to an MCP host (in this case, Claude for Desktop):

![](https://mintcdn.com/mcp/4ZXF1PrDkEaJvXpn/images/current-weather.png?w=2500&fit=max&auto=format&n=4ZXF1PrDkEaJvXpn&q=85&s=3922160478785cc88d5e98d418e8f7dd)

Servers can connect to any client. We’ve chosen Claude for Desktop here for simplicity, but we also have guides on [building your own client](https://modelcontextprotocol.io/docs/develop/build-client) as well as a [list of other clients here](https://modelcontextprotocol.io/clients).

### Core MCP Concepts

MCP servers can provide three main types of capabilities:

1. **[Resources](https://modelcontextprotocol.io/docs/learn/server-concepts#resources)**: File-like data that can be read by clients (like API responses or file contents)
2. **[Tools](https://modelcontextprotocol.io/docs/learn/server-concepts#tools)**: Functions that can be called by the LLM (with user approval)
3. **[Prompts](https://modelcontextprotocol.io/docs/learn/server-concepts#prompts)**: Pre-written templates that help users accomplish specific tasks

This tutorial will primarily focus on tools.

- Python
- TypeScript
- Java
- Kotlin
- C#
- Ruby
- Rust
- Go

Let’s get started with building our weather server! [You can find the complete code for what we’ll be building here.](https://github.com/modelcontextprotocol/quickstart-resources/tree/main/weather-server-python)

### Prerequisite knowledge

This quickstart assumes you have familiarity with:

- Python
- LLMs like Claude

### Logging in MCP Servers

When implementing MCP servers, be careful about how you handle logging:

**For STDIO-based servers:** Never write to stdout. Writing to stdout will corrupt the JSON-RPC messages and break your server. The `print()` function writes to stdout by default, but can be used safely with `file=sys.stderr`.

**For HTTP-based servers:** Standard output logging is fine since it doesn’t interfere with HTTP responses.

### Best Practices

- Use a logging library that writes to stderr or files.

### Quick Examples

```python
import sys
import logging

# ❌ Bad (STDIO)
print("Processing request")

# ✅ Good (STDIO)
print("Processing request", file=sys.stderr)

# ✅ Good (STDIO)
logging.info("Processing request")
```

### System requirements

- Python 3.10 or higher installed.
- You must use the Python MCP SDK 1.2.0 or higher.

### Set up your environment

First, let’s install `uv` and set up our Python project and environment:

```shellscript
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Make sure to restart your terminal afterwards to ensure that the `uv` command gets picked up.

Now, let’s create and set up our project:

```shellscript
# Create a new directory for our project
uv init weather
cd weather

# Create virtual environment and activate it
uv venv
source .venv/bin/activate

# Install dependencies
uv add "mcp[cli]" httpx

# Create our server file
touch weather.py
```

Now let’s dive into building your server.

## Building your server

### Importing packages and setting up the instance

Add these to the top of your `weather.py`:

```python
from typing import Any

import httpx
from mcp.server.fastmcp import FastMCP

# Initialize FastMCP server
mcp = FastMCP("weather")

# Constants
NWS_API_BASE = "https://api.weather.gov"
USER_AGENT = "weather-app/1.0"
```

The FastMCP class uses Python type hints and docstrings to automatically generate tool definitions, making it easy to create and maintain MCP tools.

### Helper functions

Next, let’s add our helper functions for querying and formatting the data from the National Weather Service API:

```python
async def make_nws_request(url: str) -> dict[str, Any] | None:
    """Make a request to the NWS API with proper error handling."""
    headers = {"User-Agent": USER_AGENT, "Accept": "application/geo+json"}
    async with httpx.AsyncClient() as client:
        try:
            response = await client.get(url, headers=headers, timeout=30.0)
            response.raise_for_status()
            return response.json()
        except Exception:
            return None

def format_alert(feature: dict) -> str:
    """Format an alert feature into a readable string."""
    props = feature["properties"]
    return f"""
Event: {props.get("event", "Unknown")}
Area: {props.get("areaDesc", "Unknown")}
Severity: {props.get("severity", "Unknown")}
Description: {props.get("description", "No description available")}
Instructions: {props.get("instruction", "No specific instructions provided")}
"""
```

### Implementing tool execution

The tool execution handler is responsible for actually executing the logic of each tool. Let’s add it:

```python
@mcp.tool()
async def get_alerts(state: str) -> str:
    """Get weather alerts for a US state.

    Args:
        state: Two-letter US state code (e.g. CA, NY)
    """
    url = f"{NWS_API_BASE}/alerts/active/area/{state}"
    data = await make_nws_request(url)

    if not data or "features" not in data:
        return "Unable to fetch alerts or no alerts found."

    if not data["features"]:
        return "No active alerts for this state."

    alerts = [format_alert(feature) for feature in data["features"]]
    return "\n---\n".join(alerts)

@mcp.tool()
async def get_forecast(latitude: float, longitude: float) -> str:
    """Get weather forecast for a location.

    Args:
        latitude: Latitude of the location
        longitude: Longitude of the location
    """
    # First get the forecast grid endpoint
    points_url = f"{NWS_API_BASE}/points/{latitude},{longitude}"
    points_data = await make_nws_request(points_url)

    if not points_data:
        return "Unable to fetch forecast data for this location."

    # Get the forecast URL from the points response
    forecast_url = points_data["properties"]["forecast"]
    forecast_data = await make_nws_request(forecast_url)

    if not forecast_data:
        return "Unable to fetch detailed forecast."

    # Format the periods into a readable forecast
    periods = forecast_data["properties"]["periods"]
    forecasts = []
    for period in periods[:5]:  # Only show next 5 periods
        forecast = f"""
{period["name"]}:
Temperature: {period["temperature"]}°{period["temperatureUnit"]}
Wind: {period["windSpeed"]} {period["windDirection"]}
Forecast: {period["detailedForecast"]}
"""
        forecasts.append(forecast)

    return "\n---\n".join(forecasts)
```

### Running the server

Finally, let’s initialize and run the server:

```python
def main():
    # Initialize and run the server
    mcp.run(transport="stdio")

if __name__ == "__main__":
    main()
```

Your server is complete! Run `uv run weather.py` to start the MCP server, which will listen for messages from MCP hosts.

Let’s now test your server from an existing MCP host, Claude for Desktop.

## Testing your server with Claude for Desktop

Claude for Desktop is not yet available on Linux. Linux users can proceed to the [Building a client](https://modelcontextprotocol.io/docs/develop/build-client) tutorial to build an MCP client that connects to the server we just built.

First, make sure you have Claude for Desktop installed. [You can install the latest version here.](https://claude.ai/download) If you already have Claude for Desktop, **make sure it’s updated to the latest version.**

We’ll need to configure Claude for Desktop for whichever MCP servers you want to use. To do this, open your Claude for Desktop App configuration at `~/Library/Application Support/Claude/claude_desktop_config.json` in a text editor. Make sure to create the file if it doesn’t exist.

For example, if you have [VS Code](https://code.visualstudio.com/) installed:

```shellscript
code ~/Library/Application\ Support/Claude/claude_desktop_config.json
```

You’ll then add your servers in the `mcpServers` key. The MCP UI elements will only show up in Claude for Desktop if at least one server is properly configured.

In this case, we’ll add our single weather server like so:

```json
{
  "mcpServers": {
    "weather": {
      "command": "uv",
      "args": [
        "--directory",
        "/ABSOLUTE/PATH/TO/PARENT/FOLDER/weather",
        "run",
        "weather.py"
      ]
    }
  }
}
```

You may need to put the full path to the `uv` executable in the `command` field. You can get this by running `which uv` on macOS/Linux or `where uv` on Windows.

Make sure you pass in the absolute path to your server. You can get this by running `pwd` on macOS/Linux or `cd` on Windows Command Prompt. On Windows, remember to use double backslashes (`\\`) or forward slashes (`/`) in the JSON path.

This tells Claude for Desktop:

1. There’s an MCP server named “weather”
2. To launch it by running `uv --directory /ABSOLUTE/PATH/TO/PARENT/FOLDER/weather run weather.py`

Save the file, and restart **Claude for Desktop**.

### Test with commands

Let’s make sure Claude for Desktop is picking up the two tools we’ve exposed in our `weather` server. You can do this by looking for the “Add files, connectors, and more /” icon:

![](https://mintcdn.com/mcp/zNouQwo2h8cbxlDS/images/visual-indicator-mcp-tools.png?w=2500&fit=max&auto=format&n=zNouQwo2h8cbxlDS&q=85&s=f6414d3ad85dfc1e37ab2dffe278c6de)

After clicking on the plus icon, hover over the “Connectors” menu. You should see the `weather` servers listed:

![](https://mintcdn.com/mcp/zNouQwo2h8cbxlDS/images/available-mcp-tools.png?w=2500&fit=max&auto=format&n=zNouQwo2h8cbxlDS&q=85&s=8298981f84cb55c6e477006cb8bf873b)

If your server isn’t being picked up by Claude for Desktop, proceed to the [Troubleshooting](#troubleshooting) section for debugging tips.

If the server has shown up in the “Connectors” menu, you can now test your server by running the following commands in Claude for Desktop:

- What’s the weather in Sacramento?
- What are the active weather alerts in Texas?
![](https://mintcdn.com/mcp/4ZXF1PrDkEaJvXpn/images/current-weather.png?w=2500&fit=max&auto=format&n=4ZXF1PrDkEaJvXpn&q=85&s=3922160478785cc88d5e98d418e8f7dd) ![](https://mintcdn.com/mcp/4ZXF1PrDkEaJvXpn/images/weather-alerts.png?w=2500&fit=max&auto=format&n=4ZXF1PrDkEaJvXpn&q=85&s=12f50039e4a1c9544a22a9bdae46f719)

Since this is the US National Weather service, the queries will only work for US locations.

## What’s happening under the hood

When you ask a question:

1. The client sends your question to Claude
2. Claude analyzes the available tools and decides which one(s) to use
3. The client executes the chosen tool(s) through the MCP server
4. The results are sent back to Claude
5. Claude formulates a natural language response
6. The response is displayed to you!

## Troubleshooting

Claude for Desktop Integration Issues

**Getting logs from Claude for Desktop**

Claude.app logging related to MCP is written to log files in `~/Library/Logs/Claude`:

- `mcp.log` will contain general logging about MCP connections and connection failures.
- Files named `mcp-server-SERVERNAME.log` will contain error (stderr) logging from the named server.

You can run the following command to list recent logs and follow along with any new ones:

```shellscript
# Check Claude's logs for errors
tail -n 20 -f ~/Library/Logs/Claude/mcp*.log
```

**Server not showing up in Claude**

1. Check your `claude_desktop_config.json` file syntax
2. Make sure the path to your project is absolute and not relative
3. Restart Claude for Desktop completely

To properly restart Claude for Desktop, you must fully quit the application:

- **Windows**: Right-click the Claude icon in the system tray (which may be hidden in the “hidden icons” menu) and select “Quit” or “Exit”.
- **macOS**: Use Cmd+Q or select “Quit Claude” from the menu bar.

Simply closing the window does not fully quit the application, and your MCP server configuration changes will not take effect.

**Tool calls failing silently**

If Claude attempts to use the tools but they fail:

1. Check Claude’s logs for errors
2. Verify your server builds and runs without errors
3. Try restarting Claude for Desktop

**None of this is working. What do I do?**

Please refer to our [debugging guide](https://modelcontextprotocol.io/docs/tools/debugging) for better debugging tools and more detailed guidance.

Weather API Issues

**Error: Failed to retrieve grid point data**

This usually means either:

1. The coordinates are outside the US
2. The NWS API is having issues
3. You’re being rate limited

Fix:

- Verify you’re using US coordinates
- Add a small delay between requests
- Check the NWS API status page

**Error: No active alerts for \[STATE\]**

This isn’t an error - it just means there are no current weather alerts for that state. Try a different state or check during severe weather.

For more advanced troubleshooting, check out our guide on [Debugging MCP](https://modelcontextprotocol.io/docs/tools/debugging)

## Next steps

## [Building a client](https://modelcontextprotocol.io/docs/develop/build-client)

Learn how to build your own MCP client that can connect to your server

## [Example servers](https://modelcontextprotocol.io/examples)

Check out our gallery of official MCP servers and implementations

## [Build with Agent Skills](https://modelcontextprotocol.io/docs/develop/build-with-agent-skills)

Use agent skills to guide AI coding assistants through server design