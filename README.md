# Caruso Recipe Book

Paste this message into **Claude Code or Codex**:

> Install and use the Caruso Recipe Book skill from https://github.com/rscboy/caruso-recipe-book. Handle setup for me, read the skill instructions, and start helping me add a recipe in this conversation. Ask me for the Recipe Book password when needed.

Your assistant reads the instructions, handles installation, and asks for the family password. Then it asks whose collection to use, takes a recipe link or pasted recipe, collects your notes and photo choice, and shows a preview. It publishes only after you say yes.

**No ZIP to manage, command file to open, manual setup commands, or restart.** The assistant can read and use the instructions immediately while installing them for future use. Publishing needs permission to contact the recipe website. Installing from GitHub alone does not grant that permission. A temporary workspace can use the instructions for its current conversation, but cannot install them on your computer.

## Package

The installable folder is [`skills/caruso-recipe-book`](skills/caruso-recipe-book). It contains Markdown instructions only, with no executable setup scripts or dependencies. The root [SKILL.md](SKILL.md) mirrors it for assistants opening this repository directly. Credentials are requested separately and saved outside the skill on your computer after verification. They are never included in this public repository.

The skill adds one approved recipe at a time through the website's add-only service. It cannot edit or delete existing recipes and does not need GitHub or deployment credentials.

## If Claude says the website is blocked

The skill cannot override your assistant's network settings. In **Claude Code cloud sessions**, edit the current cloud environment, set **Network access → Custom**, and add `www.daytongrowth.co` to **Allowed domains**, preserving existing domains and defaults. Anthropic says current sessions adopt the change within about a minute, without restarting. [Official network instructions](https://code.claude.com/docs/en/cloud-environments#network-access).

Regular Claude chat uses different settings; see [Claude's network-access guidance](https://support.claude.com/en/articles/12111783-create-and-edit-files-with-claude). If the account cannot allow this domain, publishing needs an authorized connector or another permitted client. This repository provides a skill, not an MCP connector. The assistant can still prepare the recipe while access is unresolved.
