# Dr. Mustard

A sandwich therapist. The visitor says how they feel; Dr. Mustard prescribes one sandwich.

## What is in this folder

- `index.html`: the whole site (page, styles and script).
- `api/chat.js`: the relay function. It holds the API key, Dr. Mustard's instructions and the spending caps, and passes messages to Claude.
- `vercel.json`: tells Vercel the function may run for up to 30 seconds.

## Putting it live on Vercel

1. In the Claude Console (Anthropic's site for API accounts), buy a small amount of credits, leave auto-reload off, and create an API key.
2. Put this folder in a GitHub repository, keeping `api/chat.js` inside the `api` folder.
3. In Vercel, import that repository as a new project. No framework or build settings are needed.
4. In the project's settings, add an environment variable named `ANTHROPIC_API_KEY` with the key as its value, then redeploy.

The site is then live at the address Vercel gives the project. A custom domain can be added in the project's Domains settings.

## The caps

- **Total spend:** the prepaid credit balance in the Claude Console. When it reaches zero, Dr. Mustard is "out of the office" until credits are added.
- **Per reply, per session, per visitor:** the numbers at the top of `api/chat.js`.

The per-visitor limit is kept in the function's memory, so it is best effort: it resets when Vercel recycles the function. The credit balance is the cap that cannot be exceeded.

## How much he thinks

Dr. Mustard thinks briefly before each reply, which helps him respect diets and allergies and choose a sandwich that suits the person's city. To change it, add an environment variable named `DR_MUSTARD_THINKING` set to `off`, `low`, `medium` or `high`, and redeploy. Without it the site uses `low`. `off` is about two seconds faster per reply.

## Changing the model

Add an environment variable named `ANTHROPIC_MODEL` (for example `claude-sonnet-5-5`) and redeploy. Without it the site uses `claude-haiku-5-5`.
