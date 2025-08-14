# Web Search MCP Server

A Model Context Protocol (MCP) server that enables free web searching using Google search results, with no API keys required.

## Features

- Search the web using Google search results
- No API keys or authentication required
- Returns structured results with titles, URLs, and descriptions
- Configurable number of results per search

## Getting Started

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/web-search.git
   cd web-search
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Build the server:**
   ```bash
   npm run build
   ```

4. **Configure your MCP client:**
   You need to tell your MCP client where to find the web search server.

   **For VSCode, Cursor, or other IDEs:**
   In your MCP configuration (e.g., `.mcprc.json`), add the following entry, **making sure to replace `"/path/to/web-search"` with the actual absolute path to the `web-search` directory on your computer.**

   ```json
   {
     "mcpServers": {
       "web-search": {
         "command": "node",
         "args": ["/path/to/web-search/build/index.js"]
       }
     }
   }
   ```

   **For Obsidian Users:**
   How you configure this tool in Obsidian depends on which plugin you are using.

   **If you are using the "Smart Connections" plugin:**
   1. Open Obsidian's settings.
   2. Go to "Smart Connections" under "Community Plugins".
   3. Go to the "MCP" tab.
   4. In the "MCP Servers" section, add a new server with the following configuration:
      - **Name:** `web-search`
      - **Command:** `node`
      - **Arguments:** `/path/to/web-search/build/index.js`

   **If you are using the "Model Context Protocol" plugin:**
   1. Open Obsidian's settings.
   2. Go to "Model Context Protocol" under "Community Plugins".
   3. In the "Servers" section, add a new server with the following configuration:
      - **Name:** `web-search`
      - **Command:** `node`
      - **Arguments:** `/path/to/web-search/build/index.js`

   **Important:** For both plugins, make sure to replace `/path/to/web-search` with the actual absolute path to the `web-search` directory on your computer.

   **Example:** If you cloned the repository to `/Users/jane/projects/web-search`, the path in the "Arguments" field would be `/Users/jane/projects/web-search/build/index.js`.

## Usage

The server provides a single tool named `search` that accepts the following parameters:

```typescript
{
  "query": string,    // The search query
  "limit": number     // Optional: Number of results to return (default: 5, max: 10)
}
```

Example usage:
```typescript
use_mcp_tool({
  server_name: "web-search",
  tool_name: "search",
  arguments: {
    query: "your search query",
    limit: 3  // optional
  }
})
```

Example response:
```json
[
  {
    "title": "Example Search Result",
    "url": "https://example.com",
    "description": "Description of the search result..."
  }
]
```

## Limitations

Since this tool uses web scraping of Google search results, there are some important limitations to be aware of:

1. **Rate Limiting**: Google may temporarily block requests if too many searches are performed in a short time. To avoid this:
   - Keep searches to a reasonable frequency
   - Use the limit parameter judiciously
   - Consider implementing delays between searches if needed

2. **Result Accuracy**: 
   - The tool relies on Google's HTML structure, which may change
   - Some results might be missing descriptions or other metadata
   - Complex search operators may not work as expected

3. **Legal Considerations**:
   - This tool is intended for personal use
   - Respect Google's terms of service
   - Consider implementing appropriate rate limiting for your use case

## Contributing

Feel free to submit issues and enhancement requests!
