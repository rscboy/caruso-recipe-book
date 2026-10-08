# Caruso Recipe Book

Paste this message into **Claude Code or Codex**:

> Install and use the Caruso Recipe Book skill from https://github.com/rscboy/caruso-recipe-book. Handle setup for me, read the skill instructions, and start helping me add a recipe in this conversation. Ask me for the Recipe Book password when needed.

Your assistant reads the instructions, handles installation, and asks for the family password. Then it asks whose collection to use, takes a recipe link or pasted recipe, collects your notes and photo choice, and shows a preview. It publishes only after you say yes.

**No ZIP to manage, command file to open, manual setup commands, or restart.** The assistant can read and use the instructions immediately while installing them for future use. Local Claude Code or Codex needs internet access and permission to save the skill and contact the recipe website. A temporary workspace can use the instructions for its current conversation, but cannot install them on your computer.

## Package

The installable folder is [`skills/caruso-recipe-book`](skills/caruso-recipe-book). It contains Markdown instructions only, with no executable setup scripts or dependencies. The root [SKILL.md](SKILL.md) mirrors it for assistants opening this repository directly. Credentials are requested separately and saved outside the skill on your computer after verification. They are never included in this public repository.

The skill adds one approved recipe at a time through the website's add-only service. It cannot edit or delete existing recipes and does not need GitHub or deployment credentials.
