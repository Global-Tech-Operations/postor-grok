---
name: get-started
description: Explain Postor account connection, current membership and permissions when a user installs Postor or asks about its access.
---

Use `get_account_status` to identify the connected account, organization, current
membership and OAuth permissions. If authentication is required, use the tool's
OAuth challenge and let the user sign in on Postor. Never ask for their password,
token, API key, one-time code or card information in chat.

After the user returns from authorization, make a NEW `get_account_status` call.
Never reuse an error from before sign-in, infer access from the browser alone,
or describe a connection as belonging to this conversation. Access is checked
with the selected connection's current credentials on each call. If the first
check after sign-in still reports an auth error, retry only this read once.
If it succeeds, continue the user's original request without asking them to
repeat it. If it still fails, use the host's OAuth challenge. Do not open the
generic connections/revocation page as a substitute for an OAuth flow.

`get_profile` identifies the selected connection for host account labels; its
stable ID is preserved across refresh and reconnect. `get_account_status`
separately returns live membership, company and granted permissions. Honor the
selected account; never silently switch to a different connected company.

Postor requires an existing paid membership. Explain inactive membership or
unavailable functions plainly, with the returned support contact when useful.
Do not promote plans, link checkout or offer purchases. A paid membership does
not grant every feature: honor the actual feature, role and quota result.

Read access is selected initially on Postor. Writing and deletion are separate opt-in permissions for the published actions.
Collaboration is not used by this version; do not request it. Only request additional permissions for the
specific task the user wants. Users can revoke all connections at
https://app.postor.com.mx/conexiones/chatgpt.

Company-linked `SUPER_ADMIN` accounts are supported under the same membership
rules; plugin calls have company administrator permissions, not global access.
Membership, feature and quota errors are not authentication failures. Do not
reconnect to bypass them. Missing scopes require only the permissions needed
for the current task. Never automatically retry a write after authorization:
inspect its state and preserve its requestKey.

For business-opportunity searches, inspect `list_custom_filters` and the relevant
`get_custom_filter`, then use `search_licitaciones` with `perfilId` and the
requested section. Match the user's criteria, not merely the name of a Profile.
If none fits, ask for business criteria before creating one, or use a semantic
search for the immediate request. Do not change a Profile without authorization.

Use the other Postor skills only when their workflow matches the user's task.

The plugin publishes 32 operations, each as a separate named tool with its own input schema, OAuth scope
and safety annotations. search_licitaciones and semantic_search_licitaciones
search vigente opportunities; list_custom_filters and get_custom_filter expose
the user's AI Profiles. Invoke account actions directly using their advertised
contracts; there are no hidden operations or generic execution gateways.
A host's limited tool list is not evidence of missing membership or permissions.
If one of these published tools is missing, explain that the host catalog is
incomplete and ask to refresh the plugin metadata, not to reconnect an active
account. Reconnection is only for actual OAuth failures. Additional platform
operations are not published; refreshing or reconnecting cannot enable them. Never substitute historical similarity for current search.
