---
up: 
related: 
created: 2025-06-06
tags:
  - tools/app
---



[For Server Developers - Model Context Protocol](https://modelcontextprotocol.io/quickstart/server)



```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/yangyu/Desktop",
        "/Users/yangyu/Downloads"
      ]
    },
    "sqlite": {
      "command": "uvx",
      "args": [
        "mcp-server-sqlite",
        "--db-path",
        "/Users/yangyu/Project/01-Focus/sqlite-test/sample.db"
      ]
    }
  }
}

```