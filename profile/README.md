<p align="center">
  <a href="https://www.scrapeless.com/en?utm_source=github&amp;utm_medium=referral&amp;utm_campaign=org_overview">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="./images/scrapeless-dark.png">
      <source media="(prefers-color-scheme: light)" srcset="./images/scrapeless-light.png">
      <img src="./assets/scrapeless-light.png" alt="Scrapeless — Web Infrastructure for AI Agents. Agent Browser, AI Scraper, Scraping API, Web Unlocker, Proxies." width="100%">
    </picture>
  </a>
</p>

# Scrapeless — Web Infrastructure for AI Agents

Give your agents a browser, bring live web data into your applications, and monitor what AI platforms say about your brand. Scrapeless connects browser automation, AI answer collection, and structured web data in one platform.

**[$5 Free Credit · No Credit Card Required → Sign Up](https://app.scrapeless.com/passport/login/?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** · [Website](https://www.scrapeless.com/en?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Documentation](https://docs.scrapeless.com/en/overview/?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Examples](https://github.com/scrapeless-ai/examples)

## What are you building?

| Your goal | Product | Start here |
| --- | --- | --- |
| Give an AI agent a browser to navigate, click, and complete multi-step tasks | **[Agent Browser](https://www.scrapeless.com/en/product/scraping-browser?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [CLI + agent skill](https://github.com/scrapeless-ai/scrapeless-agent-browser) |
| Track brand mentions, answers, and citations across AI platforms | **[AI Scraper](https://docs.scrapeless.com/en/llm-chat-scraper/quickstart/introduction/?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [ChatGPT product page](https://www.scrapeless.com/en/product/web-scraper/chatgpt?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Examples](#ai-answers--geo) |
| Retrieve content from public websites with anti-bot protection | **[Web Unlocker](https://www.scrapeless.com/en/product/web-unlocker?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [Agent skill](https://github.com/scrapeless-ai/webunlocker-skill) |
| Collect structured search, social, or e-commerce data | **[Scraping API](https://www.scrapeless.com/en/product/scraping-api?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [Google Search API, TikTok & Amazon ↓](#scraping-api) |
| Turn websites into content for RAG and data pipelines | **[Crawl](https://docs.scrapeless.com/en/crawl/quickstart/introduction/?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [SDK examples](https://github.com/scrapeless-ai/sdk-node/tree/main/examples) |
| Add geo-targeted IPs to your own stack | **[Proxy Solutions](https://www.scrapeless.com/en/product/proxy-solutions?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** | [Python SDK](https://github.com/scrapeless-ai/sdk-python) |

### Scraping API

Dedicated APIs for structured data from search engines, social platforms, and marketplaces.

| API | Use it for | Resources |
| --- | --- | --- |
| **Google Search API** | Search results for research agents, SEO, and competitive monitoring | [Documentation](https://docs.scrapeless.com/en/google-search-api/quickstart/introduction/?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Repository](https://github.com/scrapeless-ai/google-scraper) |
| **TikTok Scraper** | Public creator profiles, video lists, and TikTok Shop product data | [Website](https://www.scrapeless.com/en/solutions/tiktok?utm_source=github&utm_medium=referral&utm_campaign=org_overview) |
| **Amazon Scraper** | Product and search data, pricing, and Amazon Rufus responses | [Product](https://www.scrapeless.com/en/product/web-scraper/amazon?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Repository](https://github.com/scrapeless-ai/amazon-scraper) |

## Quick start: open a cloud browser

Get an API key from the [Scrapeless dashboard](https://app.scrapeless.com/passport/login/?utm_source=github&utm_medium=referral&utm_campaign=org_overview). With Node.js installed, install the browser client and set your key:

```bash
npm install puppeteer-core
export SCRAPELESS_API_KEY="YOUR_API_KEY"
```

Save this as `quickstart.mjs`, then run `node quickstart.mjs`:

```javascript
import puppeteer from 'puppeteer-core';

const key = process.env.SCRAPELESS_API_KEY;
if (!key) throw new Error('Set SCRAPELESS_API_KEY first.');
const browser = await puppeteer.connect({
  browserWSEndpoint: `wss://browser.scrapeless.com/api/v2/browser?token=${encodeURIComponent(key)}&sessionTTL=180&proxyCountry=ANY`,
});
try {
  const page = await browser.newPage();
  await page.goto('https://example.com', { waitUntil: 'domcontentloaded' });
  console.log(await page.title());
} finally {
  await browser.close();
}
```

This opens a remote browser, prints the page title, and closes the session. For terminal-based agent workflows, use the [Agent Browser CLI](https://github.com/scrapeless-ai/scrapeless-agent-browser).

## Connect your AI assistant

Use the **[MCP Server](https://github.com/scrapeless-ai/scrapeless-mcp-server)** to bring browser actions, web content, search results, and AI Scraper tasks into MCP-compatible clients such as Claude Code and Cursor.

<details>
<summary>View the MCP configuration</summary>

With Node.js installed, add this server entry using your client's MCP configuration format and replace the API key:

```json
{
  "mcpServers": {
    "scrapeless": {
      "command": "npx",
      "args": ["-y", "scrapeless-mcp-server"],
      "env": {
        "SCRAPELESS_API_KEY": "YOUR_API_KEY"
      }
    }
  }
}
```

Follow the [server setup guide](https://github.com/scrapeless-ai/scrapeless-mcp-server#setup-guide) for transport options and configuration details.

</details>

Prefer agent skills? Explore [Agent Browser](https://github.com/scrapeless-ai/scrapeless-agent-browser#usage-with-ai-agents), [Web Unlocker](https://github.com/scrapeless-ai/webunlocker-skill), and [AI Scraper](https://github.com/scrapeless-ai/llm-chat-scraper-skill). Each repository lists its supported clients and setup requirements.

## SDKs

| Language | Install | Repository |
| --- | --- | --- |
| Python | `pip install scrapeless` | [sdk-python](https://github.com/scrapeless-ai/sdk-python) |
| Node.js / TypeScript | `npm install @scrapeless-ai/sdk` | [sdk-node](https://github.com/scrapeless-ai/sdk-node) |
| Go | `go get github.com/scrapeless-ai/sdk-go` | [sdk-go](https://github.com/scrapeless-ai/sdk-go) |

See each SDK's README for supported products and usage examples.

## Integrations

- **AI frameworks:** [LangChain](https://github.com/scrapeless-ai/langchain-scrapeless) · [Dify](https://www.scrapeless.com/en/integration/scrapeless-with-dify?utm_source=github&utm_medium=referral&utm_campaign=org_overview)
- **Workflow automation:** [n8n](https://github.com/scrapeless-ai/n8n-nodes-scrapeless) · [Make](https://www.scrapeless.com/en/integration/scrapeless-with-make?utm_source=github&utm_medium=referral&utm_campaign=org_overview)
- **AI coding tools:** [Claude Code, Cursor, and other MCP clients](https://github.com/scrapeless-ai/scrapeless-mcp-server)
- **Browser automation:** [Puppeteer, Playwright, and agent frameworks](https://www.scrapeless.com/en/product/scraping-browser?utm_source=github&utm_medium=referral&utm_campaign=org_overview)

[Browse all integration guides →](https://www.scrapeless.com/en/integration?utm_source=github&utm_medium=referral&utm_campaign=org_overview)

## Explore examples

Choose a repository, configure your API key and dependencies, then follow its setup instructions.

### Agent Browser & web access

[Agent Browser CLI](https://github.com/scrapeless-ai/scrapeless-agent-browser) · [MCP browser workflows](https://github.com/scrapeless-ai/scrapeless-mcp-server) · [Web Unlocker skill](https://github.com/scrapeless-ai/webunlocker-skill)

### AI answers & GEO

Collect answers and citations for brand monitoring and AI search analysis:

[ChatGPT](https://github.com/scrapeless-ai/chatgpt-scraper) · [Perplexity](https://github.com/scrapeless-ai/perplexity-scraper) · [Gemini](https://github.com/scrapeless-ai/gemini-scraper) · [Copilot](https://github.com/scrapeless-ai/copilot-scraper) · [Grok](https://github.com/scrapeless-ai/grok-scraper) · [Google AI Mode](https://github.com/scrapeless-ai/google-ai-mode-scraper) · [Google AI Overview](https://github.com/scrapeless-ai/google-ai-overview-scraper) · [Amazon Alexa](https://github.com/scrapeless-ai/alexa-scraper) · [AI Scraper skill](https://github.com/scrapeless-ai/llm-chat-scraper-skill)

### Search & e-commerce

[Google Search API](https://github.com/scrapeless-ai/google-scraper) · [Google Trends example](https://github.com/scrapeless-ai/google-trends-scraper) · [Amazon Scraper](https://github.com/scrapeless-ai/amazon-scraper)

### RAG & data pipelines

[MCP RAG server](https://github.com/scrapeless-ai/mcp-rag-server) · [SDK and workflow examples](https://github.com/scrapeless-ai/examples)

## Open-source tools

[**Respondo**](https://github.com/scrapeless-ai/respondo) — A Python library for web scraping, text extraction, and AI-assisted parsing.

## Why Scrapeless?

- **Build agent workflows:** use cloud browsers with persistent profiles and session visibility.
- **Bring fresh context into AI:** collect web content, search data, and AI answers.
- **Reduce infrastructure work:** use managed browser, CAPTCHA, and proxy capabilities.
- **Keep your stack:** connect through SDKs, browser frameworks, MCP, and workflow integrations.
- **Expand by use case:** combine browser actions with dedicated data APIs as your application grows.

**[Claim Your $5 Free Credit · No Credit Card Required →](https://app.scrapeless.com/passport/login/?utm_source=github&utm_medium=referral&utm_campaign=org_overview)** · [Read the docs](https://docs.scrapeless.com/en/overview/?utm_source=github&utm_medium=referral&utm_campaign=org_overview) · [Explore the platform](https://www.scrapeless.com/en?utm_source=github&utm_medium=referral&utm_campaign=org_overview)
