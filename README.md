# Stooges

**If one is good, three is better.**

Stooges puts AI models from different companies to work on one question together. One model leads and writes the answer. The others review it: they point out what it missed and question what looks wrong, and the lead revises. You see the whole discussion, including where the models disagree.

- Website: [stooges.ai](https://stooges.ai)
- App: [app.stooges.ai](https://app.stooges.ai)
- MCP connector: `https://connector.stooges.ai/mcp`, see the [connector guide](connector/README.md)

This repository holds the public documentation for Stooges and its MCP connector. The Stooges source code is not here.

## Why more than one model

A single model can be confidently wrong, and it rarely catches its own mistakes. Models from different companies are trained differently, so they tend to miss different things. In Stooges they work on the same question in the open:

1. The lead drafts an answer.
2. The reviewers critique it: what is missing, what is wrong, what they would do differently.
3. The lead revises with those critiques in front of it.

Nothing is averaged or voted on, and there is no hidden judge. The answer comes out of the discussion. When the models don't agree, you see that too.

## How you use it

- **Cast it.** Choose the Stooges for your question: who leads, who reviews and, where your plan allows, which model each one runs. Save a cast you like as a preset.
- **Ask it.** Type your question and add the material it is about.
- **Watch it.** The round runs in front of you, one seat at a time. A round usually takes a few minutes.
- **Keep it.** Rounds are kept in Productions and Scenes, so you can come back and continue a line of work. Improv is for a quick question you don't need to keep.

You can also set how much the reviewers speak up (the Cowbell setting), from silent to aggressive.

## Where your work is kept

Your conversations are saved in your own storage: your Google Drive, or one GitHub repository you choose (we recommend a new, empty, private one). Stooges also keeps a working copy in its own database so it can show your history and continue a conversation. The [privacy policy](https://app.stooges.ai/privacy) has the details.

## Ways in

- **The app** at [app.stooges.ai](https://app.stooges.ai).
- **Your AI app**, through the MCP connector. Stooges has run rounds from Claude, ChatGPT, Claude Code, OpenAI Codex and Grok. See the [connector guide](connector/README.md).

## Plans

There are four plans: Open Mic, Headliner, Studio and BYOK (bring your own keys, where rounds run on your own AI provider keys and your providers bill you). Current prices and limits are at [stooges.ai](https://stooges.ai/#pricing). The connector is included in every plan.

## Stooges Jr.

Stooges for ages 10 to 17. Jailbird checks every message on the way in and every reply on the way out. Stooges Jr. is in testing, by invitation only, and is not open to the public. [stooges.ai/stooges-jr](https://stooges.ai/stooges-jr)

## Contact

stooges@docentechs.com

## Legal

- [Terms](https://app.stooges.ai/terms)
- [Privacy](https://app.stooges.ai/privacy)

Stooges™ is a product of Docent LLC. Patent pending.

Stooges is not affiliated with or endorsed by Anthropic, OpenAI, Google, xAI or Meta.
