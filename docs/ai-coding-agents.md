# Using the Rankavi API with AI Coding Agents

[Rankavi](https://rankavi.com) exposes a plain REST API secured with a Bearer API key. Any AI coding agent that can run a shell command or make an HTTP call can use it, since that is a standard capability of modern agent tooling rather than a Rankavi-specific integration.

## Claude Code

Claude Code (Anthropic's CLI coding agent) can call the Rankavi API in two ways:

- **Bash tool**: Claude Code can run shell commands, including `curl`, so it can call `POST /mentions` or `GET /categories` directly when given your API key.
- **MCP (Model Context Protocol)**: Claude Code acts as an MCP client. A small MCP server can wrap the Rankavi API as a tool (one REST endpoint per tool is a common pattern), configured in `.claude/settings.json` or `~/.claude.json`.

Example, calling the API directly via Bash:

```bash
curl -s -X POST https://app.rankavi.com/api/v1/mentions \
  -H "Authorization: Bearer $RANKAVI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "brand_name": "Acme Coffee Roasters",
    "category_id": "coffee-and-beverage",
    "target_url": "https://acmecoffee.com"
  }'
```

This is a generic REST-with-Bearer-token capability, true of Claude Code for any API with an OpenAPI spec, not a built or endorsed Rankavi integration.

## OpenAI Codex

Codex, OpenAI's agentic coding product built into ChatGPT, runs in a sandboxed environment with shell and tool-calling access. The same pattern applies: an agent task can shell out to `curl` or use a defined tool function to call `POST /mentions`, using the OpenAPI spec in this repo as the contract.

## Grok

xAI's Grok API supports function/tool calling, where you define a function schema and the model requests a call to it. Wrapping Rankavi's two endpoints as callable functions lets a Grok-based agent submit mention orders or list categories the same way.

## Why this matters for automated brand-building workflows

Because the Rankavi API accepts a simple JSON payload and returns a plain JSON order object, it fits naturally into any agent framework built around tool calling, whether that's a coding agent, a marketing automation agent, or a custom pipeline script. The full request and response shapes are documented in [`reference/openapi.yaml`](../reference/openapi.yaml), and full API docs live at [app.rankavi.com/api-docs](https://app.rankavi.com/api-docs). Get an API key from your [Rankavi](https://rankavi.com) dashboard account settings.
