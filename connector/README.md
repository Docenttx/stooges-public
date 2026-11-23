# Stooges MCP connector

Ask the Stooges from the AI app you already use. Your app sends a question to Stooges. A cast of models from different companies drafts an answer, reviews it and revises it, and the result comes back into your chat.

**Server URL**

```
https://connector.stooges.ai/mcp
```

- Transport: Streamable HTTP.
- Sign-in: OAuth with dynamic client registration. Your app opens a Stooges sign-in page; there is no API key to copy.

## Contents

- [What you need](#what-you-need)
- [Set it up](#set-it-up)
- [What you can ask for](#what-you-can-ask-for)
- [Permissions](#permissions)
- [Tools](#tools)
- [How a round works from your app](#how-a-round-works-from-your-app)
- [Long material](#long-material)
- [Usage and plans](#usage-and-plans)
- [Privacy](#privacy)
- [Disconnecting](#disconnecting)
- [Troubleshooting](#troubleshooting)

## What you need

- A Stooges account on any plan: Open Mic, Headliner, Studio or BYOK. Plans are at [stooges.ai](https://stooges.ai/#pricing).
- To start a new saved Scene from your app: Google Drive connected in your Stooges account. Improv rounds need no storage.
- An AI app that supports remote MCP servers with OAuth sign-in.

## Set it up

Stooges has run rounds from each app below. Menus in these apps change often; each section links that app's own guide.

### Claude (claude.ai and the Claude desktop app)

1. Open **Customize**, then **Connectors**.
2. Add a custom connector. Name it `Stooges` and paste the server URL.
3. Leave the sign-in settings as Claude suggests, then add it and sign in to Stooges.
4. In a chat, turn Stooges on from the **+** menu, under **Connectors**.

On Team and Enterprise, an owner adds the connector first; each member then connects their own Stooges account.

Guide: [Get started with custom connectors using remote MCP](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp)

### ChatGPT (chatgpt.com)

1. Open **Plugins** and add a custom MCP server.
2. Name it `Stooges`, paste the server URL, and choose OAuth sign-in.
3. Confirm the warning, create it, and sign in to Stooges.
4. In a chat, type `@` and pick Stooges.

Custom MCP servers depend on your ChatGPT plan, and in a workspace an admin may need to allow them. ChatGPT asks you to confirm actions such as starting a round.

Guide: [Developer mode, apps and full MCP connectors in ChatGPT](https://help.openai.com/en/articles/12584461-developer-mode-apps-and-full-mcp-connectors-in-chatgpt-beta)

### Claude Code

```
claude mcp add --transport http stooges https://connector.stooges.ai/mcp
```

Then, in Claude Code, type `/mcp`, choose `stooges`, and sign in to Stooges in your browser.

Guide: [Connect Claude Code to tools via MCP](https://code.claude.com/docs/en/mcp)

### OpenAI Codex (command-line tool and IDE extension)

```
codex mcp add stooges --url https://connector.stooges.ai/mcp
codex mcp login stooges
```

Sign in to Stooges in the browser window that opens.

Guide: [Codex MCP](https://developers.openai.com/codex/mcp)

### Grok (grok.com)

1. Open **Connectors** and choose **New Connector**, then **Custom**.
2. Paste the server URL and sign in to Stooges.

Grok shows the council's answers as text; it does not show the visual casting card.

Guide: [Grok connectors](https://docs.x.ai/grok/connectors)

### Other apps

Any app that supports remote MCP servers with OAuth sign-in may work. We add an app to this list once we have seen it run a round.

## What you can ask for

Talk to your AI app normally. For example:

- "Ask the Stooges whether this contract clause does what I think it does." (Paste or attach the clause.)
- "Open the Stooges casting call so I can pick the cast."
- "Run my saved preset called Research on this question."
- "Continue the last Stooges Scene with a follow-up: what about the edge cases?"
- "Do a quick Improv round on this; I don't need to keep it."
- "Give me the full Stooges discussion as a document."

## Permissions

When you connect, Stooges shows a sign-in and approval page with two permissions:

| Permission | On the approval page | What it allows |
| --- | --- | --- |
| `stooges:read` | See your Productions, Scenes, stooges and round results | Listing your Productions, Scenes, Stooges and presets; opening the casting call; reading rounds and their documents |
| `stooges:rounds` | Start rounds with your stooges; this uses your Stooges plan and counts toward its usage limits | Starting rounds; saving a cast; saving or deleting presets; uploading material for a round |

An app that asks for no permission at all gets `stooges:read` only. Anything that uses your plan has to be asked for by name, so it always appears on the approval page.

## Tools

In Stooges, rounds live in **Scenes**, and Scenes live in **Productions**. The tool names and arguments say "take" where the app says "Scene".

| Tool | What it does | Permission |
| --- | --- | --- |
| `stooges_list_productions` | Lists your Productions, and whether a new Scene can be created | read |
| `stooges_list_takes` | Lists the Scenes in a Production, or the rounds in a Scene | read |
| `stooges_list_cast` | Lists the Stooges your plan includes, their models, and your plan's cast size and model level | read |
| `stooges_list_presets` | Lists your saved presets, and whether each can run on your plan | read |
| `stooges_casting_call` | Opens the visual casting card to choose the lead, reviewers, models, and the Scene or Improv. Opening it asks nothing and spends nothing. Apps that cannot show the card get the same information as text | read |
| `stooges_set_cast` | Saves the cast for a Scene, or creates a new Scene with that cast | rounds |
| `stooges_save_preset` | Saves a cast as a named preset | rounds |
| `stooges_delete_preset` | Deletes one of your presets. Scenes already cast from it keep their cast | rounds |
| `stooges_stage_context` | Uploads long material in pieces and reassembles it, checked, on the server | rounds |
| `stooges_stage_upload` | Uploads a whole file in one step, for callers that can run a shell (such as Claude Code) | rounds |
| `stooges_start_round` | Asks the Stooges a question and starts a round | rounds |
| `stooges_get_round` | Reads a round: the lead's answer and the reviewers' points, or the full discussion page by page | read |
| `stooges_get_deliverable` | Returns a signed, time-limited link to the full discussion as a Markdown or HTML document | read |

## How a round works from your app

- **Start.** `stooges_start_round` returns a round id within seconds. The round itself runs for about 2 to 15 minutes: the lead drafts, the reviewers critique, and the lead revises.
- **Check back.** Your app reads the round with `stooges_get_round`. While it runs, you see the seats so far; when it finishes, you get the lead's final answer and each reviewer's points.
- **Receipts.** Every result starts with a one-line receipt that identifies the round. Your app uses it to continue the Scene or to check which round it is reading.
- **Continue.** A follow-up in the same Scene builds on its latest round. One round runs in a Scene at a time.
- **The council doesn't see your chat.** It sees the question and the material your app sends with it.
- **Web search is off unless you ask.** On the Stooges website the council can search the web by default. From your app, ask for search when a question needs current information. Search adds to the round's usage.
- **Cowbell.** Sets how often reviewers speak, from 1 (Silent) to 5 (Aggressive). Your plan may limit it; the result says so when it does.
- **Improv.** A round with no Production or Scene. It is not saved, it can be read (as a summary) for up to 24 hours, and it cannot be exported as a document.

## Long material

Chat apps limit how much text a single tool call can carry. For long material:

- **`stooges_stage_context`** sends it in pieces of about 32,000 characters. The server reassembles them, can check them against the whole file's SHA-256, and returns a reference the round uses. Sending the same piece twice changes nothing; sending a different piece under the same number is refused.
- **`stooges_stage_upload`** is for apps that can run a shell. It returns a single-use upload address, valid for 15 minutes. The file must be UTF-8 text, match the SHA-256 and size given, be no larger than 4 MB, and fit a round on your plan.

Staged material is kept for 24 hours, so another round can reuse it. Staging spends nothing and starts nothing.

## Usage and plans

- The connector is included in Open Mic, Headliner, Studio and BYOK.
- Rounds started from your app count toward your plan, just like rounds on the website.
- Results report how full a Scene is as percentages, never in money.
- On BYOK, rounds run on your own provider keys.
- Your plan decides which Stooges and models you can seat. A preset saved with more than your plan allows can run with your plan's limits applied; the result lists what changed.

## Privacy

- Stooges receives the question and any material your app sends with it, and nothing else from your conversation with that app.
- Saved rounds are stored in your own storage, as on the website, and Stooges keeps a working copy so it can show and continue your work.
- Documents from `stooges_get_deliverable` are behind signed links that expire.
- Full details: [Privacy policy](https://app.stooges.ai/privacy) and [Terms](https://app.stooges.ai/terms).

## Disconnecting

Remove the connector in your AI app's settings. Your Productions, Scenes and presets stay in your Stooges account.

## Troubleshooting

| What you see | What to do |
| --- | --- |
| A new Scene is refused because Google Drive is not connected | Connect Google Drive in your Stooges account (the result includes the link), or run an Improv round |
| A Stooge is not available on your plan | Ask your app to list the cast; it shows the Stooges your plan includes |
| A round is still running | Rounds take up to about 15 minutes. Ask your app to check again |
| A round is already running in this Scene | Wait for it to finish, then send the follow-up |
| A notice says Stooges is going down briefly for maintenance | Rounds already running finish and can still be read. Try a new round in a few minutes |
| The approval page says it belongs to another account | Sign in as the Stooges account that started the connection, or start the connection again from your app |
| Very long answers look cut off in your app | Some apps shorten long tool results. Ask for the full discussion as a document |

## Support

stooges@docentechs.com

---

Stooges™ is a product of Docent LLC. Patent pending. Stooges is not affiliated with or endorsed by Anthropic, OpenAI, Google, xAI or Meta.
