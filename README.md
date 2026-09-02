# Caruso Recipe Book

An add-only Codex and Claude Code skill for contributing one recipe at a time to the Caruso family recipe book.

## Install

Download this repository as a ZIP, attach it to Codex or Claude Code, and ask the assistant to review and install the skill. Keep the installed folder name `caruso-recipe-book`.

The owner generates a 30-day add-only guest code from the recipe website's **Add** panel. Paste that guest code into your Codex or Claude chat when the skill asks for it. The assistant uses it for local setup without repeating it. The code cannot edit or delete recipes, and it expires after 30 days; it will remain in your chat history until then.

Then run `$caruso-recipe-book` in Codex or `/caruso-recipe-book` in Claude Code.

If an AI environment blocks the recipe website, finish the interview and download the prepared JSON. Open the recipe website in a normal browser and use **Add → Publish a prepared recipe**.

## Security boundary

This package contains no GitHub, Vercel, or website credentials. Guest codes are saved only on the contributor's computer. The server validates an append-only recipe payload and rejects modifications, replacements, reordering, and deletion.

See [SKILL.md](SKILL.md) for the complete workflow.
