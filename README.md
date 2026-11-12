# Iris Works MCP server for ChatGPT and Claude

Connect Iris Works to ChatGPT, Claude and other AI agents through Cotlet. Work with clients, photography sessions, contracts and invoices in your own signed-in account. Cotlet is independent and not affiliated with Iris Works. If Iris Works offers an official API for your needs, we recommend it.

## What you can ask

> Show my upcoming photography sessions and their workflow to-dos.

> Add a session for the client and date I provide. Ask me before saving.

> Create a draft invoice for the client and session I choose. Ask me before saving; do not send it.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Claude

Add `https://cotlet.dev/mcp/v1` as a custom connector in Claude and sign in with Cotlet.dev. Follow the steps in your Cotlet console.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Iris Works tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers": {"iris-works": {"command": "python3", "args": ["/absolute/path/to/iris-works-mcp/iris_works_agent.py", "serve"], "env": {"COTLET_API_KEY": "your-key"}}}}
```

Or with Docker:

```bash
docker build -t iris-works-mcp .
docker run -i --rm -e COTLET_API_KEY iris-works-mcp
```

Tools: `iris_works_guide`, `iris_works_status`, `iris_works_open`, `iris_works_read`, `iris_works_click`, `iris_works_type`, `iris_works_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. Run from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 iris_works_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 iris_works_agent.py status    # is Iris Works ready in your Cotlet.dev account
python3 iris_works_agent.py guide     # Iris Works screens and sign-in link
python3 iris_works_agent.py read      # open Iris Works, read the page, close the browser
python3 iris_works_agent.py tools     # list Cotlet.dev tools
python3 iris_works_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Iris Works users

**How do I connect Iris Works to ChatGPT or Claude?**

Sign up at cotlet.dev, log in to Iris Works once in its Cloud Browser and add Cotlet to ChatGPT or Claude, following the steps in your console. No API key is needed. ChatGPT and Claude then work in your Iris Works account through Cotlet, in their phone apps too.

**What can ChatGPT do in Iris Works?**

ChatGPT and Claude read your leads, clients and calendar, send booking invitations, contracts and quotes, add sessions with their workflows, create and send invoices, record payments and check workflow to-dos, within your Iris Works account.

**Can ChatGPT add a session in Iris Works?**

ChatGPT adds the session for the client and date you give it and attaches its workflow, after you approve, so the workflow's emails and to-dos are scheduled.

**Does Iris Works have an API?**

No publicly documented Iris Works API was found on 11 Nov 2026: its /api and /developers pages returned 404 and the help center has no API article. Its integrations are Square, Stripe, PayPal, calendar sync, QuickBooks, Pic-Time and Fundy Designer. Cotlet works through your own Iris Works sign-in.

**Is Cotlet affiliated with Iris Works?**

No. Cotlet is independent and not affiliated with Iris Works.

## Find it on

- [Iris Works on Cotlet](https://cotlet.dev/integrations/iris-works-api-mcp-server)
- [All Cotlet packages](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/iris-works-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=iris-works

Request access: https://cotlet.dev/signup?app=iris-works&utm_source=github&utm_medium=readme&utm_campaign=iris-works
