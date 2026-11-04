# Atlas by SigmaTools — MCP connector

Connect your assistant to your Atlas training. Read permitted workout history,
build a split, suggest an exercise alternative, and prepare changes that you
review in Atlas. Approved changes are applied in the app for you.

This repository contains the open-source connector configuration and setup
documentation for the **hosted Atlas MCP service**. It contains no local server,
executable, install hook, or Atlas application/backend source.

## Connect

- **Server URL:** `https://atlas.sigmatools.io/api/ai/mcp`
- **Transport:** Streamable HTTP
- **Authentication:** OAuth through Atlas; no API key or password goes in this
  repository or a chat message.
- **Current setup guide:** [Connect your assistant](https://atlas.sigmatools.io/ai)

Use a client that supports remote MCP with OAuth and automatic client
registration. Install this connector through a compatible plugin client, or
add the server URL as a custom MCP connection. Sign into Atlas in the browser
flow, choose permissions, and allow access. Finish in the same browser that
started the connection. Confirm that the assistant can read Atlas capabilities
before asking it to change a plan.

The repository supplies a portable `plugin.json`, a Cursor manifest at
`.cursor-plugin/plugin.json`, and the shared root `mcp.json`. Client-specific
availability, account requirements, and setup controls vary; use the linked
guide for current ChatGPT, Grok, Grok Bot, and Muse instructions. Grok and Grok
Bot have separate connection settings.

### Cursor desktop

For local installation, place this repository as a real folder at
`~/.cursor/plugins/local/atlas-by-sigmatools`, then reload the Cursor window.
In **Customize → MCPs**, enable the Atlas plugin source and choose
**Authenticate**. Complete Atlas consent in the browser while Cursor is waiting
for the callback. If an earlier attempt expired, restart Authenticate.

Use **Agent mode** and approve the requested Atlas tool calls. In the tested
Cursor version, Ask mode discovered the tools but blocked their execution.
If you already configured the same Atlas URL manually, Cursor groups the sources;
select the intended source so you know which connection you are testing.

Marketplace installation remains subject to review and listing availability.
See [Cursor’s local-plugin instructions](https://cursor.com/docs/plugins#test-plugins-locally).

### Account requirements and price

Atlas access requires an adult account with setup completed, current Atlas
Terms accepted, and active Premium or an eligible trial. There is
no separate fee for this connector package. Assistant subscriptions and
availability are controlled by the assistant provider.

### Android setup with Grok

If authorizing from a mobile browser opens the Grok app instead of completing
the browser connection, Android may be handing the return link to the app.
Temporarily turn off **Open supported links** under Android Settings → Apps →
Grok → Open by default (sometimes called Set as default). Restart connection
setup at [grok.com/connectors](https://grok.com/connectors) in the same browser,
and restore your preferred link setting afterward. Alternatively, establish
the connection in a desktop browser. An established connection can then be
used from supported mobile clients on the same assistant account; confirm Atlas
is available there. Atlas cannot override another app's Android link settings.

## What you can ask

- “Look at my recent training and summarize what changed.”
- “Build me a four-day split using my dumbbells and bench.”
- “Move next week's workouts to Monday, Wednesday, Friday and Saturday.”
- After explicitly sharing a workout: “That machine is taken. What else can I
  do with the equipment available?”
- After explicitly sharing a workout: “I have fifteen minutes left. Suggest
  changes to the remaining unlogged work.”

The assistant can search the Atlas exercise catalog and propose supported
routine, split, calendar, or shared-session changes. Suggestions are not saved
merely because the assistant says they are ready: open the proposal in Atlas,
review it, and apply it. Atlas checks permissions and whether its source data
has changed before application.

## Permissions

You choose permissions in Atlas. Existing connections do not automatically gain
new permissions; reconnect if you want to add them.

| Scope | What it permits |
| --- | --- |
| `training:read` | Read bounded synced completed-workout history and training summaries. |
| `routines:read` | Read saved cloud routines and exercise targets. |
| `routines:propose` | Propose new routines for review; this scope alone does not edit existing routines. |
| `plan:read` | Read the saved routine library, training prescriptions, splits, and selected calendar dates. |
| `sessions:read` | Read temporary workout snapshots you explicitly share from an Atlas device. |
| `training:propose` | Propose supported training changes for review. Saved-plan changes also require `plan:read`; shared-session changes also require `sessions:read` and a current snapshot. |

Completed-history reads are limited to up to 60 recent synced sessions within
the last 90 days. Private notes, photos, billing details, and social content are
not exposed by these permissions.

### Shared workouts and approvals

Shared-session access is a snapshot, **not a live stream**. A snapshot lasts up
to 15 minutes. To apply a session proposal, return to Atlas on the **same device
that shared it**, while the snapshot is valid and its source workout still
matches. If the workout changed or the snapshot expired, share it again and
request a fresh proposal. Saved-plan proposals are reviewed in Atlas too.

The connector cannot rewrite completed workouts or XP, permanently delete
routines, publish social posts, or change billing/security settings. Each
proposed training change requires your review in Atlas.

Access can last up to 30 days. Refresh tokens operate within that grant period;
they do not extend its expiry. Reconnect when the grant expires. Disconnect at
[Settings → AI connections](https://atlas.sigmatools.io/settings/connections)
to stop future access and block pending proposals. Disconnecting cannot recall
information already received by the assistant.

## Verification status

These are bounded workflow checks of the hosted service, not certification of
every client, tool, or device:

| Client | Recorded verification |
| --- | --- |
| Grok Bot | October 30, 2026: permitted reads; reviewed routine create/update/archive/restore; shared-session preparation and adjustment; stale-change refusal; client-visible denial after test disconnection. |
| ChatGPT web | October 31, 2026: permitted reads; reviewed routine creation and archive; shared-session preparation and adjustment; cleanup and a reconnect prompt after test disconnection. The tested client required manual tool confirmations. |
| Muse | November 1–2, 2026: permitted reads; reviewed routine creation; reviewed unlogged-session exercise swap; cleanup and an unauthorized response after test disconnection. |
| Cursor desktop | November 4, 2026: local plugin installation and OAuth; all 12 tools discovered; permitted reads; routine creation reviewed and applied in Atlas; saved readback and reviewed archive cleanup; a fresh client call returned Unauthorized after test disconnection. The tested client required Agent mode and manual tool confirmations. Marketplace installation is not yet verified. |

The recorded checks used dedicated synthetic test data. They do not establish
marketplace acceptance, a cross-account penetration test, or universal mobile
setup compatibility. The Grok Bot and ChatGPT disconnection observations do not
claim captured raw server or refresh-token rejection. No tester credentials,
identifiers, callbacks, or private training payloads are included here.

## Support and license

- [Atlas](https://atlas.sigmatools.io/)
- [Setup guide](https://atlas.sigmatools.io/ai)
- [Terms](https://atlas.sigmatools.io/terms)
- [Privacy](https://atlas.sigmatools.io/privacy)
- [Health disclaimer](https://atlas.sigmatools.io/health-disclaimer)
- Support: [hello@sigmatools.io](mailto:hello@sigmatools.io)
- Security reports: see [SECURITY.md](SECURITY.md).

Connector configuration and documentation are available under the [MIT
license](LICENSE). The hosted Atlas application is a separate service governed
by its terms; this repository does not license its proprietary implementation.
The logo and trademark rights are covered by [TRADEMARKS.md](TRADEMARKS.md).
