# Alexein AI for Antigravity

Gives your Antigravity agents your [Alexein](https://alexein.ai) memory: they search what you have told Alexein before
answering, and save what they learn as you work, so the next session, and your other apps, pick up where this one
left off.

## One memory across your AI tools

Alexein is your own memory, not your agents's. Connect it to the other AI tools you use too (Claude, ChatGPT,
Cursor, GitHub Copilot and more) and they all share it: a preference you mention in one, a decision you make in
another, or a detail about your project is there for your agents the next time it matters, and the other way round.
It also holds what you chose to connect to Alexein, such as Slack, GitHub or email, so answers can come from your
team's conversations and past decisions, not only this chat.

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

## Recall and saving sessions

The plugin also adds hooks for the Antigravity CLI (`hooks.json`) and an always-on rule, `rules/AGENTS.md`, with the note on how to use the memory tools. Until they are signed in they only keep that rule; nothing is read or sent.

They need the plugin signed in to your Alexein account. The first time a session starts without it, your
browser opens Alexein's sign-in, where you choose **Allow**; nothing is copied or pasted. If you close it, it
opens again at most once a day (once a week after **Cancel**), and
`python3 <plugin>/scripts/alexein_hooks.py run antigravity sign-in` opens it whenever you like. The key it makes is a
personal key labelled **Antigravity · your computer's name**, listed under **My memory › Keys**, and kept in
`~/.alexein/hooks/antigravity/`, readable only by you. Instead, a key of your own can go in `ALEXEIN_API_KEY` (a personal
key from **My memory › Keys**, **Read and write**; or `api_key` in `~/.config/alexein/hooks.json`).

Signed in, or with a key:

- **Recall.** The first message of each session is looked up in your memory and the best matches are added as
  context before the model is called. One search per session.
- **Saving sessions.** What you ask and the agent's final replies are saved to your memory, with the names of files
  changed and commands run (never their contents or output), five exchanges at a time. Anything that looks like a
  password, key or token is removed first. `ALEXEIN_CAPTURE=false` keeps recall and saves nothing.

Three behaviours are off unless their environment variable is `1`, while they are measured: with
`ALEXEIN_RECALL_EVERY_PROMPT` a later message on a new topic is looked up too; with `ALEXEIN_RECALL_BEFORE_EDIT`
the first edit of a file brings what memory holds about it before the model's next step; with `ALEXEIN_ASK_CATCH` a reply that ends by asking you something memory may hold is sent back once to look first. Each adds only what bears on what was asked, at most
about 600 tokens, and waits at most 2.5 seconds. `ALEXEIN_SIGN_IN=0` keeps the sign-in from opening on its own.

`python3 <plugin>/scripts/alexein_hooks.py run antigravity pause` (or `resume`, `status`) turns this off and on. The
hooks need `python3`; they are the same script as the Claude Code plugin's
([claude-plugins](https://github.com/Alexein-AI/claude-plugins)).
