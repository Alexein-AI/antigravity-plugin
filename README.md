# Alexein AI for Antigravity

Gives your Antigravity agents your [Alexein](https://alexein.ai) memory: they search what you have told Alexein before
answering, and save what they learn as you work, so the next session, and your other apps, pick up where this one
left off.

## Install

```
agy plugin install https://github.com/Alexein-AI/antigravity-plugin
```

When Antigravity first connects to Alexein, it opens Alexein's sign-in in your browser. Sign in (or create a free
account at [memory.alexein.ai](https://memory.alexein.ai)), choose what the agent may do (read only, or read and
save), and select **Allow**. No API key is needed.

## What it adds

One MCP server, `memory` (shown as `alexein-ai_memory`), at `https://api.alexein.ai/v1/mcp`. Its tools search your
memory, open what it holds, and save new facts; the full list is at
[docs.alexein.ai/mcp/tools](https://docs.alexein.ai/mcp/tools).

Everything saved can be seen, downloaded and erased in the Alexein app, under **My memory**. To disconnect, remove the
plugin, or disconnect Antigravity in the Alexein app under **AI assistants**.

## Help

[docs.alexein.ai/mcp](https://docs.alexein.ai/mcp) · zainali@alexein.ai · [Privacy](https://alexein.ai/legal/privacy) ·
[Terms](https://alexein.ai/legal/terms)

## Recall and saving sessions (optional API key)

The plugin also adds hooks for the Antigravity CLI (`hooks.json`) and an always-on rule, `rules/AGENTS.md`, with the note on how to use the memory tools. Without an API key they only keep that rule; nothing is read or sent.

With a key in `ALEXEIN_API_KEY` (a personal key from **My memory › Keys** in the Alexein app, **Read and write**;
or `api_key` in `~/.config/alexein/hooks.json`):

- **Recall.** The first message of each session is looked up in your memory and the best matches are added as
  context before the model is called. One search per session.
- **Saving sessions.** What you ask and the agent's final replies are saved to your memory, with the names of files
  changed and commands run (never their contents or output), five exchanges at a time. Anything that looks like a
  password, key or token is removed first. `ALEXEIN_CAPTURE=false` keeps recall and saves nothing.

`python3 <plugin>/scripts/alexein_hooks.py run antigravity pause` (or `resume`, `status`) turns this off and on. The
hooks need `python3`; they are the same script as the Claude Code plugin's
([claude-plugins](https://github.com/Alexein-AI/claude-plugins)).
