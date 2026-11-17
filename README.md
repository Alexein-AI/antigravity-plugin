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
