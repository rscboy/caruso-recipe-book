# Owner setup and sharing

This is the one-time setup for the website owner. Contributors do not need GitHub or Vercel access.

Share the starter message from the recipe website. It points to `https://github.com/rscboy/caruso-recipe-book`. The assistant reads the instructions, installs the skill, asks for the contributor password when needed, verifies access, and handles the recipe interview and publishing. No separate installer or restart is required for that flow.

Optional installed copies can use the `caruso-recipe-book` folder in the contributor's local skill directory. Keep the folder name unchanged for native skill discovery.

Configure these server-side environment variables in the production Vercel project:

- `CARUSO_RECIPE_ADD_TOKEN`: the add-only Recipe Book password issued to contributors.
- `CARUSO_RECIPE_GITHUB_TOKEN`: a fine-grained GitHub token or GitHub App token with Contents write access only to `rscboy/daytongrowthco`.
- `CARUSO_RECIPE_GITHUB_REPOSITORY`: optional; defaults to `rscboy/daytongrowthco`.
- `CARUSO_RECIPE_GITHUB_BRANCH`: optional; defaults to `main`.
- `CARUSO_RECIPE_SITE_URL`: optional; defaults to the production recipe-book URL.

Give invited contributors the starter message and the add-only password. The assistant verifies and saves the local connection described in [connection.md](connection.md). Managed installations may instead supply:

- `CARUSO_RECIPE_API_URL=https://www.daytongrowth.co/api/caruso-recipe-book`
- `CARUSO_RECIPE_ADD_TOKEN=<the invited-contributor token>`

Local connections are stored at `~/.config/caruso-recipe-book/credentials.json` with user-only file permissions.

Do not place the token in the skill files or a Git repository. Rotate `CARUSO_RECIPE_ADD_TOKEN` to revoke previously shared access. Because one shared token cannot identify or revoke a single person, use a separate gateway or per-user token table if individual revocation or auditing is required later.

The server-side GitHub credential is intentionally never distributed. The public token can call only this route; the route constructs an append-only commit to the recipe source and optional dish-image path.
