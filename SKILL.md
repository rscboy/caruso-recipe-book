---
name: caruso-recipe-book
description: Guide a family member through connecting to the Caruso Recipe Book, preparing one recipe, and publishing it after approval. Use for recipe contributions; never edit or delete existing recipes.
---

# Caruso Recipe Book

Take care of connection setup, interview the contributor, prepare one recipe, and publish only after they approve. Contributors only need to paste the starter message and answer your questions. Do not send them away to install software, run Terminal commands, restart their assistant, or download and execute setup scripts.

## Read this skill and its references

The public source is https://github.com/rscboy/caruso-recipe-book. The installable skill is `skills/caruso-recipe-book/`. Read its plain-text files from GitHub, or use the hosted copy at https://www.daytongrowth.co/recipe-book/caruso-recipe-book/SKILL.md. Resolve linked references relative to the skill file's location, not the current project directory. Read [references/connection.md](references/connection.md) for connection setup and HTTP requests, and [references/recipe-schema.md](references/recipe-schema.md) before preparing a recipe payload.

When the user asks to install, handle installation yourself using an available trusted skill installer, or copy the inspected skill's Markdown files into `~/.claude/skills/caruso-recipe-book/` for Claude Code or the configured Codex skills directory (normally `~/.codex/skills/caruso-recipe-book/`). Preserve unrelated skills and keep credentials outside that folder. This package has no executable setup scripts. If an older version exists, update only this skill's instruction files. Read the instructions and continue in the current conversation immediately, even if the client's skill menu has not refreshed. Do not require a restart. In a temporary workspace, use the instructions for this conversation and do not claim a permanent installation on the user's computer.

Use your available HTTP tools or an available runtime's standard library. No downloaded executable code or third-party packages are needed. A web-reading tool can read the instructions, but publishing requires a client that supports authenticated HTTP requests. Installation success does not prove access to the recipe service. If access is blocked, follow the connection reference's blocked-network guidance before offering a prepared recipe. Never claim setup or publishing succeeded, bypass restrictions, or claim that moving to a local session guarantees access.

## Connect for the contributor

Use the connection reference to check for existing local credentials. If the connection is unavailable or unauthorized, ask: **“What is the Recipe Book password?”** Wait for the user's answer. Verify it with an authenticated GET to the add-only recipe service. Do not guess a password or extract one from the website. After verification, save the connection privately on the contributor's computer when local file access is available. In temporary environments, explain only when relevant that the connection may need to be supplied again.

Use the returned recipe owner names for the first interview question. Keep the password out of replies, recipe files, skill files, command arguments, URLs, and logs. Never ask for a GitHub token, Vercel token, general account password, or deployment credential.

## Ask the recipe questions

Ask one question at a time and wait for the answer. Accept answers supplied in advance and ask only for what is missing.

1. **“Whose recipes are you adding it to?”** Offer the service's returned people, followed by “Add somebody else.” For a new person, ask their display name and derive a lowercase hyphenated ID and initials.
2. **“What is the link to the recipe, or would you rather copy and paste it here?”** Read an accessible public recipe URL or accept pasted text. If the URL is inaccessible, ask for the recipe text instead.
3. **“Are there any special notes or instructions I should include?”** “No” is a complete answer.
4. **“Is there a specific image you want me to use for the dish?”** Accept an HTTPS image URL, an attached JPG/PNG/WebP, or “no.” If no image is supplied, choose a relevant reusable HTTPS image and identify it in the preview.

After these answers, normalize the recipe using the schema reference. Preserve quantities, temperatures, timing, attribution, and special notes. Do not silently invent missing safety-critical temperatures. Choose a specific unique slug. Put source attribution and the user's notes in `recipe.note`. For an attached image, encode it only when preparing the confirmed addition.

Show a concise preview with the owner, title, source, image choice, and special notes. Then ask: **“Ready for me to add this recipe and publish it to the website?”** Wait for an explicit yes. Invoking this skill or supplying the password does not authorize publishing.

## Publish one confirmed recipe

POST the schema's JSON payload to the add-only service using the connection reference. The service appends a recipe and optionally a new person to the canonical website source, then starts its normal production deployment. It cannot update or delete an existing recipe.

On success, report the recipe URL, the returned commit URL, and that the website update has started. Check the recipe URL for a bounded period; claim it is live only when the new recipe is present. If still deploying, provide the link and say the update is underway. Never resubmit a successful addition.

On a timeout or lost response, the recipe may already have been added: verify the recipe URL or ask the website owner to check before retrying. On a rejected request, report the service's safe error and correct the payload only within the user's approved recipe scope.

## Add-only boundary

- Add exactly one recipe per confirmed run.
- Never edit, replace, reorder, or delete an existing recipe or person.
- Never use repository or deployment access as a fallback.
- If asked to modify or delete recipes, explain that the family skill only adds recipes.
- Connection settings and password files belong outside the skill and recipe files.

For owner maintenance of server-side configuration, read [references/owner-setup.md](references/owner-setup.md). Ordinary contributors do not need that reference.
