<div align="center">

<a href="https://www.lobstack.ai/download">
  <img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/lobstack.jpg" alt="Lobstack: Asks before it acts. An AI team on your computer, free for Windows, Mac and Linux. Beside it, the Lobstack app holding a file change for approval." width="900">
</a>

<br>

### An AI team that asks before it acts.

Lobstack runs bots on your computer. They work in your repos and tools, and they
wait for your yes before anything that changes something.
The Lobstack API behind it puts a receipt on every call.

<br>

[**Download the app**](https://www.lobstack.ai/download) · [The API](https://www.lobstack.ai/api-platform) · [Docs](https://www.lobstack.ai/docs) · [Pricing](https://www.lobstack.ai/pricing)

</div>

<br>

---

<br>

## The Lobstack app

A desktop app for Windows, macOS and Linux. You message a bot like a colleague,
and it does the job in your real tools.

- **It asks first.** Steps that only read run straight through. Writing a file,
  running a command or pushing code waits for you to press Approve.
- **It works where you work.** Your repos, your files, and the services you
  connect with one-click sign-in. It can search and read the web.
- **It hands you the finished thing.** Bots can write Word and PDF documents,
  with real charts, and keep them in your Library.
- **It keeps working.** Routines run on a schedule while the app is open.

**Free to download.** Your first sign-in from the app adds $5 of credit for 30
days, with no card. After that it runs on the Free plan, or on a paid plan.
The app uses the Lobstack API by default; GitHub Copilot or your own provider
key also work.

It is a public beta. It is not code-signed yet, so Windows warns once on the
first run and macOS needs a right-click → Open the first time.

[**Download →**](https://www.lobstack.ai/download)

<br>

## The Lobstack API

One OpenAI-compatible endpoint for 26 models from 9 providers. Keep the OpenAI
SDK you already use and change the base URL and the key:

```
https://www.lobstack.ai/api/gateway/v1
```

Send `model: "auto"` and Nex, the router inside the API, scores the request and
serves it from the cheapest tier that can answer it, never above your plan's
ceiling. A model you name is a ceiling too, not a command.

Every call comes back with a receipt: in response headers on a normal call, and
on the final stream frame under `x_lobstack` when you stream.

```json
{
  "request_id": "2f1c…",
  "served_model": "gemini-3.8-flash",
  "requested_model": "claude-opus-5",
  "routed": true,
  "priced": true,
  "cost_usd": 0.003281,
  "savings_usd": 0.018594,
  "baseline_model": "claude-opus-5",
  "baseline_reason": "named",
  "baseline_cost_usd": 0.021875
}
```

Two rules keep that number honest:

- **`cost_usd` is `null`, never `0`, when the price is unknown.** Zero would say
  the call was free.
- **A saving always says what it was measured against.** `named` means you asked
  for a model and a cheaper one served it. `plan_ceiling` means you sent `auto`
  and the comparison is the priciest model your plan allows.

[**The API →**](https://www.lobstack.ai/api-platform) · [Every model and its rate](https://www.lobstack.ai/models) · [Quickstart](https://www.lobstack.ai/docs/quickstart)

<br>

## The Console

The Console is your account: API keys, usage, logs, clients and webhooks, with
what every call cost. [Open it →](https://www.lobstack.ai/dashboard)

<br>

---

<br>

## For developers

Three public repositories, all MIT, all on npm. None is needed to call the API;
the OpenAI SDK works as it is.

| | What it is |
|---|---|
| **[lobstack-gateway](https://github.com/Lobstack-ai/lobstack-gateway)**<br><sub>`@lobstack-ai/gateway`</sub> | A typed TypeScript client for the Lobstack API, plus the published contract: `spec/openapi.yaml` for the endpoints and errors, `spec/x_lobstack.schema.json` for the receipt. |
| **[lobstack-cli](https://github.com/Lobstack-ai/lobstack-cli)**<br><sub>`lobstack`</sub> | The Lobstack API from your terminal. `chat` streams the answer to stdout and the receipt to stderr. `proxy` runs a local OpenAI-compatible endpoint, so Cursor, Aider or Continue go through Lobstack without holding your key. No dependencies. |
| **[lobstack-mcp](https://github.com/Lobstack-ai/lobstack-mcp)**<br><sub>`@lobstack-ai/mcp`</sub> | An MCP server for Claude Desktop, Claude Code, Cursor, Zed, or anything that speaks MCP over stdio. Route preview needs no key, so an agent can ask where a prompt would go and what it would cost before you have an account. |

<br>

---

<br>

## What we do not claim

- Lobstack holds **no SOC 2 or other audited certification**.
  [Security](https://www.lobstack.ai/docs/security) says what runs today and what
  is only written down.
- The [status page](https://www.lobstack.ai/status) is computed from real request
  traffic, not synthetic checks. We publish no uptime figure outside a contract.
- Every price in the [model list](https://www.lobstack.ai/models) carries the date
  it was last checked against the provider's own page.

<br>

---

<br>

<div align="center">

**hello@lobstack.ai**

Issues on the three public repositories are read. If an API call went wrong,
include the `x-lobstack-request-id` from the response. Every request gets one,
even a 401.

<br>

[Website](https://www.lobstack.ai) ·
[Download](https://www.lobstack.ai/download) ·
[API](https://www.lobstack.ai/api-platform) ·
[Docs](https://www.lobstack.ai/docs) ·
[Pricing](https://www.lobstack.ai/pricing) ·
[Status](https://www.lobstack.ai/status) ·
[About](https://www.lobstack.ai/about)

</div>
