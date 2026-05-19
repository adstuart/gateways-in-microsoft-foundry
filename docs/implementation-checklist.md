# Implementation checklist

Use this checklist before you move an AI gateway, model router, WAF, or MCP design into production.

## Scope

- [ ] Name the workload owner, platform owner, and security owner.
- [ ] Classify the workload as public, internal, regulated, or experimental.
- [ ] Define whether the endpoint serves models, agents, tools, or all three.
- [ ] Define non-goals, such as "no third-party model endpoints" or "no autonomous write actions."

## Identity and access

- [ ] Use Microsoft Entra ID or another trusted identity provider for callers.
- [ ] Use managed identity for Azure backends where supported.
- [ ] Remove raw model keys from application code.
- [ ] Scope each app, agent, and tool to least privilege.
- [ ] Validate JWT audience, issuer, expiry, and required claims at the gateway.
- [ ] Separate read-only tools from write-capable tools.

## Gateway policy

- [ ] Put shared AI traffic through APIM when more than one team or app consumes the backend.
- [ ] Apply token limits, not only request-count limits.
- [ ] Apply quotas by consumer, app, team, or business unit.
- [ ] Configure backend pools, retries, and circuit breakers for resilience.
- [ ] Decide whether semantic caching is allowed for the data sensitivity and response type.
- [ ] Decide which prompts and completions can be logged.

## Safety and data governance

- [ ] Use Prompt Shields or an equivalent control for direct and indirect prompt attacks.
- [ ] Validate model outputs before downstream systems execute or render them.
- [ ] Apply Purview, DLP, labels, or equivalent controls to sensitive data sources.
- [ ] Enforce retrieval ACLs and security trimming for RAG workloads.
- [ ] Test for prompt injection, data exfiltration, and unsafe output handling.

## Model router

- [ ] Decide whether prompt-aware model selection is allowed for the workload.
- [ ] Choose routing mode: Balanced, Cost, or Quality.
- [ ] Use model subsets if compliance, region, context length, or capability requirements restrict eligible models.
- [ ] Check region, deployment type, and rate-limit support in current documentation.
- [ ] Use direct model deployments when the workload must use one fixed model.

## WAF and edge

- [ ] Use WAF and DDoS controls for public HTTP endpoints.
- [ ] Configure request size, method, path, and rate controls.
- [ ] Do not treat WAF approval as AI security approval.
- [ ] Add AI-specific controls for prompt, response, token, tool, and agent risks.

## MCP and tools

- [ ] Register approved MCP servers and tools in a catalog.
- [ ] Route remote MCP access through APIM or an equivalent gateway.
- [ ] Validate all tool parameters against approved schemas.
- [ ] Pin tool versions and require review before metadata or schema changes.
- [ ] Log tool calls with correlation IDs.
- [ ] Require human approval for high-impact actions.

## Observability and operations

- [ ] Emit token metrics by consumer and workload.
- [ ] Trace model calls, agent decisions, and tool calls with correlation IDs.
- [ ] Alert on token spikes, loop-like behavior, repeated policy failures, and backend throttling.
- [ ] Define a kill-switch for compromised or runaway agents.
- [ ] Test failover, quota exhaustion, and content-safety blocking before launch.
