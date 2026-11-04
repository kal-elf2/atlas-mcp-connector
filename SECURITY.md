# Security

## Report a vulnerability

Send a private report to [hello@sigmatools.io](mailto:hello@sigmatools.io) with
“Atlas MCP security report” in the subject. Include the affected client/version,
reproduction steps, expected and observed behavior, and a redacted screenshot
if useful. Do not post credentials, access or refresh tokens, authorization
codes, callback URLs, or customer training data in a public issue.

Please use an account and data you are authorized to test. Do not access other
users' data, disrupt the hosted service, or publish a working exploit before
we have had a chance to investigate.

## Package boundary

This package is declarative configuration for a hosted MCP endpoint. It has no
local executable, install script, hook, dependency, embedded secret, or custom
proxy. Its MCP destination is `https://atlas.sigmatools.io/api/ai/mcp`.
Authentication and authorization are handled by the hosted service and the
client's OAuth flow. The backend is not included in this repository.

Atlas scopes data to the signed-in account and the permissions selected during
consent. Training mutations are proposals requiring explicit review in Atlas.
Shared-session proposals also depend on a current device-owned snapshot. These
controls do not mean an assistant provider cannot retain data already sent to
it; review that provider's policies before allowing access.

If a connection looks unfamiliar, disconnect it in Atlas Settings → AI
connections. Disconnection blocks future access and pending proposals. For
help with failed browser returns, follow the current
[connection guide](https://atlas.sigmatools.io/ai); never copy an authorization
callback or a token into a chat or public issue.

Use the latest connector release and a current assistant client. The hosted
service evolves separately from this configuration package. A package manifest
validation or successful client workflow is not a complete security audit of
the service.
