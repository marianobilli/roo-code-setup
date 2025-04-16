# Roo Code Online Research System for Windows

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green)

> A powerful AI-driven online research and knowledge management system for Windows, built on Roo Code and MCP servers.

## 🔍 Overview

This repository provides a complete setup for an advanced Online Research System using Roo Code custom modes and MCP servers on Windows. The system transforms simple queries into comprehensive research, automatically gathering, extracting, organizing, and indexing information from across the web.

**Key capabilities:**
- Transform natural language questions into optimized search queries
- Automatically scrape and extract relevant information from websites
- Organize findings into structured knowledge documents
- Build and maintain a searchable knowledge index

## ✨ Features

### 🌐 Online Research Mode

The **Online Research** mode is the core of this system, serving as the entry point to the knowledge management pipeline:

- **Query Optimization**: Transforms user questions into search-optimized queries
- **Concept Identification**: Extracts key concepts and selects appropriate search operators
- **Query Variations**: Creates multiple query variations (primary, broader, alternative)
- **Relevance Maximization**: Ensures high-precision search results

### 📊 Knowledge Pipeline

The system includes a complete knowledge processing pipeline:

1. **Knowledge Source Fetcher**: Retrieves content from optimal sources
2. **Knowledge Content Extractor**: Identifies and extracts relevant information
3. **Knowledge Organizer**: Structures information into well-organized documents
4. **Knowledge Indexer**: Maintains a comprehensive, searchable knowledge index

## 🚀 Quick Start

### Prerequisites

- Windows 10/11
- Visual Studio Code with Roo Code extension
- Node.js (for npx command)
- PowerShell 5.1 or later

### Installation

1. Clone this repository:
```powershell
git clone https://github.com/yourusername/roo-code-online-research.git
cd roo-code-online-research
```

2. Set up required MCP servers (API keys required for some services):
```powershell
# Store Brave Search API key
cmdkey /generic:MCP_BRAVE /user:mcp /pass:YOUR_BRAVE_API_KEY

# Store Firecrawl API key
cmdkey /generic:MCP_FIRECRAWL /user:mcp /pass:YOUR_FIRECRAWL_API_KEY
```

3. Configure Roo Code:
   - Copy `mcp_settings.json` to `%APPDATA%\Code\User\globalStorage\rooveterinaryinc.roo-cline\settings\`
   - Copy `custom_modes.json` to the same directory

4. Restart VS Code and activate the Online Research mode

## 📖 Documentation

Detailed documentation is available in the following files:

- [MCP Servers Setup](mcp-servers.md): Windows-specific installation and configuration for all required MCP servers
- [Custom Modes Configuration](custom-modes.md): How to customize and extend the research modes
- [Configuration Reference](mcp_settings.json): Example configuration for all MCP servers

### Using the Research System

1. Start with the Online Research mode
2. Enter your research question or topic
3. The system will automatically:
   - Generate optimized search queries
   - Retrieve relevant content from the web
   - Extract and organize key information
   - Present structured research results

## 🛠️ System Architecture

The Online Research System consists of:

1. **Roo Code Custom Modes**: Specialized AI assistants with defined roles
2. **MCP Servers**: External tools providing web search, scraping, and processing capabilities
3. **Knowledge Pipeline**: A series of processing stages for information retrieval and organization

### Required MCP Servers

| Server | Purpose | Configuration |
|--------|---------|--------------|
| Brave Search | Web search capabilities | [Setup Instructions](mcp-servers.md#brave-search) |
| Firecrawl | Web scraping and data extraction | [Setup Instructions](mcp-servers.md#firecrawl-mcp-server) |
| Sequential Thinking | Structured problem-solving | [Setup Instructions](mcp-servers.md#sequential-thinking) |
| GitHub (optional) | Repository management | [Setup Instructions](mcp-servers.md#github) |

## Additional Custom Modes

In addition to the Online Research mode and Knowledge Pipeline modes, this repository includes other custom modes whose instructions have been specifically optimized for non-thinking models. These modes provide complementary capabilities:

| Mode | Name | Description |
|------|------|-------------|
| **orchestrator** | ⚡️ General Purpose Orchestrator | Strategic workflow orchestrator that coordinates complex tasks by delegating them to appropriate specialized modes |
| **spec-pseudocode** | 📋 Specification Writer | Captures full project context—functional requirements, edge cases, constraints—and translates that into modular pseudocode with TDD anchors |
| **architect** | 🏗️ Architect | Designs scalable, secure, and modular architectures based on functional specs and user needs |
| **code** | 🧠 Code | Writes clean, efficient, modular code based on pseudocode and architecture |
| **debug** | 🪲 Debugger | Troubleshoots runtime bugs, logic errors, or integration failures by tracing, inspecting, and analyzing behavior |
| **security-review** | 🛡️ Security Reviewer | Performs static and dynamic audits to ensure secure code practices |
| **tech-docs-writer** | 📚 Technical Documentation Writer | Writes concise, clear, and modular Markdown documentation |
| **ask** | ❓ Ask | Task-formulation guide that helps users navigate, ask, and delegate tasks to the correct modes |
| **devops** | 🚀 DevOps | Automation and infrastructure specialist responsible for deploying, managing, and orchestrating systems |

Each mode follows a structured, step-by-step approach with explicit instructions optimized for models without advanced reasoning capabilities. This ensures consistent performance and reliable results even with simpler AI systems.

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📧 Contact

For questions or support, please open an issue in this repository.
