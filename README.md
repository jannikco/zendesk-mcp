# Zendesk MCP server

Review support tickets and create a new ticket with an initial customer-service comment.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `ZENDESK_EMAIL_WITH_TOKEN_SUFFIX`
- `ZENDESK_API_TOKEN`
- `ZENDESK_SUBDOMAIN`



Credential help: https://support.zendesk.com/hc/en-us/articles/4408889192858

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call zendesk_list_tickets '{}'
```

## Use with an MCP client

Launch `node /absolute/path/zendesk-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| zendesk_list_tickets | Read | zendesk list tickets |
| zendesk_get_ticket | Read | zendesk get ticket |
| zendesk_create_ticket | Explicit approval required | zendesk create ticket |

## Concrete workflow

Review support tickets and create a new ticket with an initial customer-service comment.

1. zendesk_list_tickets
2. zendesk_get_ticket
3. zendesk_create_ticket

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=zendesk&integration=zendesk-mcp&utm_source=github&utm_campaign=github-zendesk-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/zendesk/).

## Provenance and maintenance

- https://developer.zendesk.com/api-reference/ticketing/tickets/tickets/

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
