# Source map and deduplication notes

This repository consolidates five earlier research threads into one public guide. The goal is to preserve the learning while removing duplicate explanations, unpublished source history, bulky media, and draft-only material.

| Original thread | Canonical home in this repo | Deduplication decision |
|---|---|---|
| APIM AI gateway brief | [APIM AI gateway](apim-ai-gateway.md) and README decision summary | Kept the core point that AI gateway is APIM capabilities for AI traffic, not a separate product. Removed repeated capability tables. |
| WAF for AI workload | [WAF and AI firewalls](waf-and-ai-firewalls.md) | Kept the decision framework. Moved APIM content to the APIM page and MCP content to the MCP page. |
| Foundry model routing comparison | [Model router vs APIM](model-router-vs-apim.md) | Kept the layer distinction and patterns. Removed long model lists that age quickly. |
| OWASP agentic mitigation patterns | [OWASP control map](owasp-control-map.md), [MCP and tool governance](mcp-tool-governance.md), and [Implementation checklist](implementation-checklist.md) | Kept reusable control patterns. Removed long incident narratives and duplicated risk descriptions. |
| OWASP agentic reference | [OWASP control map](owasp-control-map.md) | Kept the Microsoft control mapping. Did not copy video assets or microsite files. |

## Public-facing edits

- Removed private source history.
- Removed bulky generated video assets.
- Removed non-public repository links.
- Kept only public Microsoft, OWASP, and vendor references.
- Rewrote content as stable guidance rather than session notes.
- Applied Microsoft-style terminology, including Microsoft Entra ID, use, allowlist, blocklist, active voice, and sentence-style headings.
