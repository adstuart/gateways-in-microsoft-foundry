# Azure API Management AI gateway

The AI gateway in Azure API Management is a set of APIM capabilities for AI traffic. It is not a separate gateway product to deploy beside APIM.

Use it when you need a governed front door for models, agents, MCP servers, A2A APIs, and tool endpoints.

## What APIM adds to AI workloads

| Capability | Why it matters |
|---|---|
| Import AI endpoints | Bring OpenAI-compatible APIs, Anthropic Messages APIs on supported tiers, Foundry APIs, MCP servers, A2A APIs, self-hosted endpoints, and third-party endpoints into one API management plane. |
| Identity and credentials | Use managed identities for Azure backends and credential manager or OAuth flows for tool and API access. Keep raw model keys out of application code. |
| Token limits and quotas | Enforce limits by subscription, user, app, team, or another policy key. This protects shared model capacity and controls cost. |
| Prompt-token prechecks | Estimate prompt tokens at the gateway and reject oversized prompts before they reach the model. |
| Content safety | Apply AI Content Safety checks, including Prompt Shields, consistently at the gateway. |
| Semantic caching | Cache semantically similar prompt responses with Azure Managed Redis or another compatible external cache. |
| Backend routing | Use APIM backends for priority, weighted, round-robin, or session-aware load balancing. |
| Resiliency | Use retries and circuit breakers to avoid sending traffic to unhealthy or throttled backends. |
| Observability | Emit token metrics, log prompts and completions when policy allows it, and send telemetry to Azure Monitor or Application Insights. |
| MCP governance | Expose REST APIs as MCP servers or govern existing remote MCP servers through APIM policies. |

## Policy examples to know

| Policy area | Example policies |
|---|---|
| Token limits | `llm-token-limit`, `azure-openai-token-limit` |
| Token metrics | `llm-emit-token-metric`, `azure-openai-emit-token-metric` |
| Semantic caching | `llm-semantic-cache-lookup`, `llm-semantic-cache-store` |
| Content safety | `llm-content-safety` |
| Classic API controls | `validate-jwt`, rate limits, quotas, IP filtering, caching, request and response validation |

Policy availability varies by APIM tier and service update channel. Check current Microsoft Learn pages before relying on a policy in a design.

## When APIM is the right control

Use APIM AI gateway when at least one of these is true:

- Multiple applications or teams share model capacity.
- You need per-team or per-user quotas and showback.
- You need one place to apply Prompt Shields or content safety checks.
- You need to fail over across model deployments, regions, or providers.
- You need developer onboarding, subscriptions, products, or a catalog.
- You need to govern MCP servers or A2A APIs used by agents.
- You need consistent logging and monitoring for AI calls.

## When APIM is not enough

APIM is a gateway and policy plane. It does not replace:

- Secure application design and output validation.
- Microsoft Purview data governance.
- Microsoft Entra ID governance for users, workloads, and agents.
- Foundry evaluations, tracing, and model monitoring.
- Secure software supply chain controls for plugins, models, and MCP servers.
- Human approval for high-impact agent actions.

## Design notes

### Prefer managed identity where possible

For Azure AI backends, use managed identities instead of raw keys. For external tools and APIs, use OAuth and credential manager where supported.

### Make token budgets explicit

Request-count rate limiting is not enough for LLMs. A single request can consume far more tokens than another request. Use token-aware limits and budget alerts.

### Treat logging as a data-governance decision

Prompt and completion logs can contain sensitive data. Decide what to log, how long to retain it, who can read it, and whether redaction is required before enabling detailed logging.

### Route for policy first, then optimize

Use APIM to decide which approved backend pool a workload can reach. Use model router inside Foundry when you also want per-prompt model selection within an approved boundary.
