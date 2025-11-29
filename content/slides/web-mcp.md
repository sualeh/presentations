---
marp: true
draft: true
theme: uncover
headingDivider: 2
paginate: true
style: |
  section {
    text-align: left;
    font-size: 32px;
  }
  ul, ol, li {
    font-size: 100%;
  }
_class:
 - lead
 - invert
---


# WebMCP

AI-Powered Web Tools in the Browser


## What is WebMCP?

- W3C standard exposing JavaScript tools to AI
- Supported by Google and Microsoft
- Runs fully in user’s browser
- Designed for human-in-the-loop


## Human-in-the-Loop
- WebMCP doesn’t replace website UI
- Tools assist users
- Users maintain control
- Collaborative workflows between humans and AI
- Respects user session and authentication


## What WebMCP is NOT

- Not for headless browsing
- Not for fully autonomous agents
- Not backend-only service integration
- Does not replace a website's human user interface


## Why Use WebMCP?

- Avoids fragile UI automation
- No OAuth or backend changes required
- Fast, deterministic calls
- User retains full control


## How WebMCP Works

- Register JavaScript functions as tools
- AI discovers and calls tools in browser
- Tools execute with user permissions
- Supports safe, collaborative workflows


## Add to Cart Example

```js
const { McpServer, TabServerTransport} = window.MCP;

const server = new McpServer({name: "shopping-site", version: "1.0"});

server.tool(
  "addToCart", 
  "Add an item to the shopping cart", 
  {
    productId: z.string().describe("Product ID"),
    quantity: z.number().min(1).describe("Quantity to add"),
  },
  async ({ productId, quantity }) => { /* Call add to cart logic */ }
);
```


## How This Example Works

- MCP server runs in browser, exposes `addToCart` tool
- AI calls `addToCart` with specified inputs
- Tool runs your application logic
- Executes under existing user session and authentication
- Enables AI agents to reliably help with cart actions


## What is `TabServerTransport`?

- In-browser transport connecting MCP server to AI agents in the same tab
- Uses `window.postMessage` for secure messaging in tab context
- Allows fast, permissioned communication (no backend or network hops)
- Restricts by allowed origins for security


## WebMCP vs. Alternatives

| Approach           | Speed | Reliability | Auth Model | Human Control | Backend Needed |
|--|--|--|--|--|--|
| Browser Automation | Slow  | Low         | Complex    | Minimal       | No            |
| Remote MCP         | Fast  | High        | OAuth2.1   | Optional      | Yes           |
| **WebMCP**         | Fast  | High        | Browser    | Built-in      | No            |
