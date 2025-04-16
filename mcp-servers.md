# MCP Servers for Roo Code in VSCode (Windows Edition)

This document provides information about recommended Model Context Protocol (MCP) servers for use with Roo Code in VSCode on Windows, including their functionality and installation instructions.

## Table of Contents

1. [Introduction](#introduction)
2. [Software Prerequisites](#software-prerequisites)
3. [Secure Credential Storage](#secure-credential-storage)
4. [Recommended MCP Servers](#recommended-mcp-servers)
5. [Firecrawl MCP Server](#firecrawl-mcp-server)
6. [Brave Search](#brave-search)
7. [Sequential Thinking](#sequential-thinking)
8. [GitHub](#github)
9. [Additional Resources](#additional-resources)

## Introduction <a name="introduction"></a>

Model Context Protocol (MCP) servers extend the capabilities of AI assistants like Roo Code by providing access to external data sources, tools, and services. These servers follow a standardized protocol that enables secure, two-way communication between AI models and external systems.

For configuration examples of all MCP servers, refer to the [mcp_settings.json](mcp_settings.json) file in the roo-code directory. This file provides a complete reference implementation that you can customize for your environment.

## Software Prerequisites <a name="software-prerequisites"></a>

To use MCP servers on Windows, you'll need:

1. **Node.js**: Install from [Node.js website](https://nodejs.org/en/download) to get access to the `npx` command
2. **PowerShell**: Already included with Windows 10/11 (ensure you're using PowerShell 5.1 or later)
3. **Windows Terminal** (optional but recommended): Install from the [Microsoft Store](https://www.microsoft.com/en-us/p/windows-terminal/9n0dx20hk701)

## Secure Credential Storage <a name="secure-credential-storage"></a>

> **IMPORTANT**: Never hardcode sensitive information such as passwords, API keys, or tokens directly in your VSCode configuration files. Instead, use secure credential storage solutions.

### Using Windows Credential Manager

Windows Credential Manager is the recommended approach for storing sensitive credentials on Windows systems.

#### Storing credentials

1. Open Command Prompt or PowerShell as Administrator
2. Store your credential:
```powershell
cmdkey /generic:MCP_SECRET_NAME /user:USERNAME /pass:YOUR_SECRET_KEY
```

Replace:
- `MCP_SECRET_NAME` with a name for your secret (e.g., `MCP_GITHUB_TOKEN`)
- `USERNAME` with a username identifier (can be any value, e.g., `mcp`)
- `YOUR_SECRET_KEY` with your actual secret key or token

#### Retrieving credentials in scripts

You can retrieve stored credentials in PowerShell scripts:

```powershell
# Create a helper function to get credentials
function Get-StoredCredential {
    param (
        [string]$Target
    )

    $output = cmdkey /generic:$Target
    if ($output -match "User: (.*)\s+Password: (.*)") {
        return $Matches[2]
    }
    return $null
}

# Use the function
$apiKey = Get-StoredCredential -Target "MCP_SECRET_NAME"
```

### Using Environment Variables

You can also use environment variables for credential storage:

#### Setting environment variables temporarily

```powershell
# Set in PowerShell before running
$env:API_KEY="your_secret_key"
```

#### Setting environment variables permanently

1. Open Start menu and search for "Environment Variables"
2. Select "Edit the system environment variables"
3. Click "Environment Variables" button
4. Under "User variables", click "New"
5. Enter the variable name (e.g., `GITHUB_TOKEN`) and value
6. Click "OK" to save

#### Using in MCP server configuration

```json
{
  "mcpServers": {
    "server-name": {
      "command": "powershell",
      "args": [
        "-Command",
        "& { $env:API_KEY=$env:STORED_API_KEY; npx -y your-mcp-server }"
      ],
      "env": {
        // Only non-sensitive configuration here
      }
    }
  }
}
```

## Recommended MCP Servers <a name="recommended-mcp-servers"></a>

| Server | Functionality | GitHub Link |
|--------|--------------|-------------|
| Firecrawl | Web scraping, crawling, search, and data extraction | [mendableai/firecrawl-mcp-server](https://github.com/mendableai/firecrawl-mcp-server) |
| Brave Search | Web and local search capabilities | [modelcontextprotocol/servers/src/brave-search](https://github.com/modelcontextprotocol/servers/tree/main/src/brave-search) |
| Sequential Thinking | Structured problem-solving through thought sequences | [modelcontextprotocol/servers/src/sequentialthinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking) |
| GitHub | Repository management and code operations | [modelcontextprotocol/servers/src/github](https://github.com/modelcontextprotocol/servers/tree/main/src/github) |

## Firecrawl MCP Server <a name="firecrawl-mcp-server"></a>
### Functionality
Firecrawl MCP Server integrates with [Firecrawl](https://github.com/mendableai/firecrawl) to provide powerful web scraping capabilities:

- Web scraping with JavaScript rendering
- URL discovery and crawling
- Web search with content extraction
- Batch processing with built-in rate limiting
- Smart content filtering
- Structured data extraction

### Setup for Windows
1. Register at https://www.firecrawl.dev/ and obtain an API KEY
2. Store your API key securely using Windows Credential Manager:
```powershell
cmdkey /generic:MCP_FIRECRAWL /user:mcp /pass:YOUR_FIRECRAWL_API_KEY
```
3. Create a PowerShell script to run the server (e.g., `run-firecrawl-mcp.ps1`):
```powershell
$env:FIRECRAWL_API_KEY = (cmdkey /generic:MCP_FIRECRAWL | Select-String "Password: (.*)").Matches.Groups[1].Value
npx -y firecrawl-mcp
```
4. Add the configuration to roo-code `mcp_settings.json` file:
```json
{
  "mcpServers": {
    "firecrawl": {
      "command": "powershell",
      "args": ["-File", "path\\to\\run-firecrawl-mcp.ps1"],
      "env": {}
    }
  }
}
```

## Brave Search <a name="brave-search"></a>

### Functionality

Brave Search MCP Server integrates with the Brave Search API to provide:

- Web search with pagination and filtering
- Local search for businesses and services
- Flexible result filtering
- Smart fallbacks from local to web search

### Setup for Windows
1. Register at https://brave.com/search/api/ and obtain an API KEY
2. Store your API key securely using Windows Credential Manager:
```powershell
cmdkey /generic:MCP_BRAVE /user:mcp /pass:YOUR_BRAVE_API_KEY
```
3. Create a PowerShell script to run the server (e.g., `run-brave-mcp.ps1`):
```powershell
$env:BRAVE_API_KEY = (cmdkey /generic:MCP_BRAVE | Select-String "Password: (.*)").Matches.Groups[1].Value
npx -y @modelcontextprotocol/server-brave-search
```
4. Add the configuration to roo-code `mcp_settings.json` file:
```json
{
  "mcpServers": {
    "brave-search": {
      "command": "powershell",
      "args": ["-File", "path\\to\\run-brave-mcp.ps1"],
      "env": {}
    }
  }
}
```

## Sequential Thinking <a name="sequential-thinking"></a>

### Functionality

Sequential Thinking MCP Server provides a tool for dynamic and reflective problem-solving:

- Break down complex problems into manageable steps
- Revise and refine thoughts as understanding deepens
- Branch into alternative paths of reasoning
- Adjust the total number of thoughts dynamically
- Generate and verify solution hypotheses

### Setup for Windows
1. Add the configuration to roo-code `mcp_settings.json` file:
```json
{
  "mcpServers": {
    "sequentialthinking": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sequential-thinking"],
      "env": {}
    }
  }
}
```

## GitHub <a name="github"></a>

### Functionality

GitHub MCP Server provides integration with the GitHub API:

- File operations (create, read, update)
- Repository management
- Issue and PR handling
- Code search
- Branch management
- Comprehensive error handling

### Setup for Windows
1. Register at https://github.com and obtain a Personal Access Token
2. Store your API key securely using Windows Credential Manager:
```powershell
cmdkey /generic:MCP_GITHUB /user:mcp /pass:YOUR_GITHUB_PERSONAL_ACCESS_TOKEN
```
3. Create a PowerShell script to run the server (e.g., `run-github-mcp.ps1`):
```powershell
$env:GITHUB_TOKEN = (cmdkey /generic:MCP_GITHUB | Select-String "Password: (.*)").Matches.Groups[1].Value
npx -y @modelcontextprotocol/server-github
```
4. Add the configuration to roo-code `mcp_settings.json` file:
```json
{
  "mcpServers": {
    "github": {
      "command": "powershell",
      "args": ["-File", "path\\to\\run-github-mcp.ps1"],
      "env": {}
    }
  }
}
```

## Additional Resources <a name="additional-resources"></a>

- [Model Context Protocol Documentation](https://modelcontextprotocol.io/)
- [MCP Server Finder](https://www.mcpserverfinder.com/)
- [Smithery MCP Server Registry](https://smithery.ai/servers)
