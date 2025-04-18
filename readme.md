# Roo Code Online‑Research & Knowledge‑Pipeline **v2**

![Version](https://img.shields.io/badge/version-1.1.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows-brightgreen)
![License](https://img.shields.io/badge/license-MIT-green)

> A token‑efficient AI research & knowledge‑management stack for Windows powered by **Roo Code** custom modes and MCP servers.

---

## 🔍 What’s new in v2 ?

| Area | Before | Now |
|------|--------|-----|
| **Online‑research** | 10‑step, 400‑line prompt | 3‑step prompt that instantly spawns the pipeline |
| **Knowledge pipeline** | Disabled by default | Streamlined 4‑stage flow auto‑called by online‑research |
| **All modes** | “EXACT / STEP N” boiler‑plate | Lean numbered lists (< 700 tokens each) |
| **Non‑reasoning model support** | Medium | ★ Optimized for fast/light LLMs |

---

## ✨ Key Components

### 🌐 Online‑Research Mode (v2)
The single entry point.  
1. Parse the user query (topic, dates, geo).  
2. Build **Primary / Broader / Alternative** search strings (≤ 150 chars).  
3. Immediately delegate to **Knowledge‑Source‑Fetcher** via `new_task`.

### 📊 Knowledge Pipeline 2 → 5

| Stage | Mode | Purpose |
|-------|------|---------|
| 1 | **knowledge‑source‑fetcher** | Run Brave Search, score relevance, fetch top 3 pages with Firecrawl |
| 2 | **knowledge‑content‑extractor** | Strip boiler‑plate, pull headings, paragraphs, code, data; label High/Med/Low |
| 3 | **knowledge‑organizer** | Auto‑choose document template (General / Comparison / Process) → Markdown file with YAML front‑matter |
| 4 | **knowledge‑indexer** | Update `~/knowledge/index.md`, `tags.md`, and `search-index.json` |

The whole flow is automatic—no user intervention needed after the initial question.

---

## 🛠️ Quick Start

### Requirements
* Windows 10/11, VS Code + Roo Code extension  
* Node.js, PowerShell 5.1+  
* Brave Search & Firecrawl API keys

### Install
```powershell
git clone https://github.com/yourusername/roo-code-online-research.git
cd roo-code-online-research
:: store API keys
cmdkey /generic:MCP_BRAVE    /user:mcp /pass:YOUR_BRAVE_API_KEY
cmdkey /generic:MCP_FIRECRAWL /user:mcp /pass:YOUR_FIRECRAWL_API_KEY
