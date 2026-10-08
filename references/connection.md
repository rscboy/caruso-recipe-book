# Recipe Book connection

## Service and local credentials

The only authorized endpoint is `https://www.daytongrowth.co/api/caruso-recipe-book`. Use HTTPS, reject redirects, and never send the password to another origin or endpoint. Requests should time out after about 30 seconds. Use the contributor's provided password as the bearer token.

If local file access is available, look for `~/.config/caruso-recipe-book/credentials.json`. An existing connection has this shape:

```json
{"apiUrl":"https://www.daytongrowth.co/api/caruso-recipe-book","addToken":"USER_PROVIDED_PASSWORD"}
```

Environment variables `CARUSO_RECIPE_ADD_TOKEN` and `CARUSO_RECIPE_API_URL` may provide the same connection; accept only the canonical URL above. Do not print environment values or credentials. If no credentials are available, ask the user for the Recipe Book password.

Verify the password with GET before saving or replacing local credentials. On `401`, ask the user to check their password. On a network failure or other service error, stop the connection attempt and report it; do not overwrite an existing working configuration or repeatedly retry.

After successful verification, save only the canonical URL and token to the local credentials file, using user-only file permissions (0600 on Unix). Create its directory if needed. Do not save credentials into the skill, repository, recipe payload, or a downloadable file. Do not put the password directly in command arguments. Use your existing tool or runtime to keep it in private process memory or read it from the protected local file. Installation into an assistant's skills directory is optional; reading these instructions works in the current conversation without restarting.

If running in a remote or temporary workspace, keep credentials only for the current session and do not claim they are saved on the user's computer or in their Claude/Codex account settings.

## Read the current people

Send GET to the canonical endpoint with the header `Authorization: Bearer <password>`. The response is:

```json
{"ok":true,"owners":[{"id":"sammy","name":"Sammy"}]}
```

Use the actual returned people, not the example above. A successful owner lookup verifies the connection without publishing anything.

## If the workspace blocks the website

Distinguish a website `401` (wrong password) from a sandbox/proxy denial or unavailable network permission. Do not ask for a password until there is a permitted client that can contact the canonical service. Do not infer the exact Claude surface from the phrase "temporary cloud workspace": ask whether this is regular Claude chat or Claude Code in the cloud if it is unclear.

For Claude Code in an Anthropic-hosted cloud environment, the contributor can open the cloud/environment selector, edit their current environment, choose **Network access → Custom**, and add **www.daytongrowth.co** to **Allowed domains**. Preserve the existing allowed domains and default package-manager list. Shared environments need their owner to make this change. The official documentation says existing sessions adopt network changes within about a minute without a new session: https://code.claude.com/docs/en/cloud-environments#network-access. Ask the contributor to make this change; never silently change network permissions or advise enabling every domain. After they confirm it, try a bounded connection check again.

For regular Claude chat, code execution uses a different network policy. Direct them to **Settings → Capabilities** (or organization settings for managed accounts), and consult https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude. Availability and domain controls depend on the account; do not present Claude Code's environment selector as a chat setting. If the account cannot permit this domain, explain that an authorized connector or another permitted client is required for publishing. This skill does not include an MCP connector.

Offer to continue preparing the recipe in the current conversation while access is unresolved. If owner lookup is unavailable, ask whose collection to use without claiming any cached names are the current list. Explain that the recipe has not been published. Do not invent a browser upload feature, claim a downloaded file will publish itself, or promise that a reinstall or restart will remove the network restriction.

## Publish after approval

Send POST to the same canonical endpoint, with `Authorization: Bearer <password>` and `Content-Type: application/json`. The body is the JSON described in [recipe-schema.md](recipe-schema.md). You may use an available authenticated HTTP tool, Python's standard library, Node's built-in fetch, or another already available HTTP client. Write or inspect the request yourself; do not download and execute a setup script or install dependencies.

Never place the password in the payload or URL. Only a successful service response with `ok: true` confirms publication. Report the returned `recipeUrl` and `commitUrl` when present. A timeout or lost response is an uncertain outcome; verify before retrying. Do not publish a test recipe during setup.
