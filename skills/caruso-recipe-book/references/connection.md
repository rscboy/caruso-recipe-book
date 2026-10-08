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

## Publish after approval

Send POST to the same canonical endpoint, with `Authorization: Bearer <password>` and `Content-Type: application/json`. The body is the JSON described in [recipe-schema.md](recipe-schema.md). You may use an available authenticated HTTP tool, Python's standard library, Node's built-in fetch, or another already available HTTP client. Write or inspect the request yourself; do not download and execute a setup script or install dependencies.

Never place the password in the payload or URL. Only a successful service response with `ok: true` confirms publication. Report the returned `recipeUrl` and `commitUrl` when present. A timeout or lost response is an uncertain outcome; verify before retrying. Do not publish a test recipe during setup.
