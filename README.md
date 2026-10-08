# Caruso Recipe Book

Paste this into Claude Code or Codex, in **Local or Cloud**:

> Use the Caruso Recipe Book skill from https://github.com/rscboy/caruso-recipe-book. Help me prepare my recipe and give me a browser review link. Do not connect to the recipe service from this workspace; I will enter the password and approve it on the website.

Your assistant asks whose collection to use, takes your recipe and notes, and gives you **Review and add your recipe**. Open that link, check the recipe, enter the family password, and click **Add this recipe**. You can choose your own photo there.

The browser handles publishing, so the assistant's cloud network restrictions do not block it. No ZIP to manage, command file, connector setup, network-setting change, or restart. Reading the skill is enough to begin; saving it locally for future conversations is optional. The browser must reach the website.

The [review page](https://www.daytongrowth.co/recipe-book/add.html) also accepts copied recipe JSON when a link is too large. No downloaded files are needed.

## Package

The installable folder is [skills/caruso-recipe-book](skills/caruso-recipe-book). This package contains instructions only, with no executable setup scripts or dependencies. The root [SKILL.md](SKILL.md) mirrors it. Contributors never need repository write access or deployment credentials.

The link contains the recipe, never a password. Anyone with it can read that prepared recipe. Publication requires the family password and the contributor's explicit browser approval. The existing add-only service cannot edit or delete recipes.
