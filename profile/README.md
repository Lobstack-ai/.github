<div align="center">

<a href="https://www.lobstack.ai">
  <img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/hero.png" alt="Lobstack — Building the agentic stack" width="900">
</a>

<br>

### One OpenAI-compatible key. Every model.<br>A receipt on every call.

One key reaches **26 models across 9 providers** — Anthropic, OpenAI, Google, xAI,
DeepSeek, Mistral, Groq, Qwen and Moonshot — through an OpenAI-compatible endpoint.
Name a model and you get it. Ask for `auto` and the request is scored for complexity
and served by the cheapest model that can answer it, never above your plan's ceiling.

<br>

[**Start free**](https://www.lobstack.ai/signup) · [Docs](https://www.lobstack.ai/docs) · [Pricing](https://www.lobstack.ai/pricing) · [Status](https://www.lobstack.ai/status) · [Compare](https://www.lobstack.ai/compare)

</div>

<br>

---

<br>

<div align="center"><h2>The products</h2></div>

<table>
<tr>
<td width="50%" valign="top">
<a href="https://www.lobstack.ai/gateway"><img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/gateway.jpg" alt="The Gateway scoring a request and choosing a tier" width="100%"></a>
<h3>Gateway</h3>
<p>One endpoint, every model, a receipt on every call. <code>POST</code> to <code>/api/gateway/v1/chat/completions</code> with the OpenAI SDK you already have — change the base URL and the key, change nothing else.</p>
<a href="https://www.lobstack.ai/gateway"><b>Explore Gateway →</b></a>
</td>
<td width="50%" valign="top">
<a href="https://www.lobstack.ai/console"><img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/console.jpg" alt="The Console showing requests, tokens and spend" width="100%"></a>
<h3>Console</h3>
<p>Watch what ran, what it cost, and what it would have cost. Every call that reached the API, true p50/p95/p99, a failure taxonomy that says whose problem it is, and spend priced when it was spent.</p>
<a href="https://www.lobstack.ai/console"><b>Explore Console →</b></a>
</td>
</tr>
<tr>
<td width="50%" valign="top">
<a href="https://www.lobstack.ai/lob-bot"><img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/lobbot.jpg" alt="Lob Bot pausing at an approval before writing a file" width="100%"></a>
<h3>Lob Bot &nbsp;<sub><code>PRERELEASE</code></sub></h3>
<p>Agents on your own machine, with a gate before anything changes. A Slack-shaped desktop app where bots hold channels, talk to each other, and stop at an approval before they touch a file.</p>
<a href="https://www.lobstack.ai/lob-bot"><b>Explore Lob Bot →</b></a>
</td>
<td width="50%" valign="top">
<a href="https://www.lobstack.ai/nex"><img src="https://raw.githubusercontent.com/Lobstack-ai/.github/main/profile/assets/nex.png" alt="A request being routed to one of several models" width="100%"></a>
<h3>Nex &nbsp;<sub><code>IN TRAINING</code></sub></h3>
<p>Our own model, learning where every request is worth sending. Its first shipped piece is the learned router — a classifier trained on what the Gateway already records about model choice.</p>
<a href="https://www.lobstack.ai/nex"><b>Read the plan →</b></a>
</td>
</tr>
</table>

<br>

---

<br>

<div align="center"><h2>The receipt</h2></div>

Most gateways route. The question worth asking is what comes back when the router
picks for you. On Lobstack it is this, on every response — headers on a buffered
call, and on the final SSE frame under `x_lobstack` when you stream:

```json
{
  "request_id": "2f1c…",
  "served_model": "gemini-3.8-flash",
  "requested_model": "claude-opus-5",
  "routed": true,
  "cost_usd": 0.003281,
  "savings_usd": 0.018594,
  "baseline_model": "claude-opus-5",
  "baseline_reason": "named",
  "baseline_cost_usd": 0.021875
}
```

Two rules hold that together, and they are why the number is worth reading.

> **`cost_usd` is `null`, never `0`, when the price is unknown.**
> A model the registry does not carry, or a stream that ended before it could be
> metered, records an absence. Zero is a claim — that the call was free — and it
> is the wrong one.

> **A saving never travels without the reason it exists.**
> `baseline_reason` says what the comparison was measured against: `named` when
> you asked for a specific model and routing chose a cheaper one, and a saving is
> only reported when there is a real baseline to subtract from.

<br>

---

<br>

<div align="center"><h2>Open source</h2></div>

Three repositories, all MIT, all on npm.

| | What it is |
|---|---|
| **[lobstack-cli](https://github.com/Lobstack-ai/lobstack-cli)**<br><sub>`lobstack`</sub> | The Gateway from your terminal. `chat` streams the answer to stdout and the receipt to stderr, so a redirect gives you the answer alone. `proxy` binds a local OpenAI-compatible endpoint, so Cursor, Aider or Continue route and meter through Lobstack without ever holding your key. Zero dependencies. |
| **[lobstack-mcp](https://github.com/Lobstack-ai/lobstack-mcp)**<br><sub>`@lobstack-ai/mcp`</sub> | An MCP server for Claude Desktop, Claude Code, Cursor, Zed, or anything else that speaks the protocol over stdio. Route preview needs no credential at all, so an agent can ask where a prompt would go and what it would cost before you have an account. |
| **[lobstack-gateway](https://github.com/Lobstack-ai/lobstack-gateway)**<br><sub>`@lobstack-ai/gateway`</sub> | A typed SDK and, more usefully, the published contract it speaks — `spec/openapi.yaml` for the endpoints and their error classes, `spec/x_lobstack.schema.json` for the receipt. A receipt nobody can validate is a quirk; a receipt with a schema is a contract. |

Versions are read out of the registry by the site rather than typed here, because
a version number in a README is a number that goes stale silently:
[lobstack.ai/docs/cli](https://www.lobstack.ai/docs/cli).

<br>

---

<br>

<div align="center"><h2>What is not claimed here</h2></div>

Lobstack is early, and the pages that would normally hide that instead say so.

- The [status page](https://www.lobstack.ai/status) computes availability from real
  request traffic rather than synthetic probes, and reports **no data** where there
  is not enough of it to report anything else.
- The model catalogue carries the date every price was last checked against the
  provider's own page, and flags any rate that could not be confirmed.
- SOC 2 Type II controls are mapped with audit-ready documentation. **No audit has
  been performed and the certification is not claimed** —
  [security](https://www.lobstack.ai/docs/security) states which controls run and
  which are written down and not deployed.
- [Compare](https://www.lobstack.ai/compare) grades the competition on four questions
  and does not put Lobstack in the table, because a vendor scoring itself in its own
  matrix always wins and everyone reading knows it.

<br>

---

<br>

<div align="center">

**hello@lobstack.ai**

Issues on the three public repositories are read. If a Gateway call went wrong,
include the `x-lobstack-request-id` from the response — every request carries one,
allocated before anything can fail, so even a 401 comes back with an id worth quoting.

<br>

[Website](https://www.lobstack.ai) ·
[Docs](https://www.lobstack.ai/docs) ·
[Gateway API](https://www.lobstack.ai/docs/gateway) ·
[Routing](https://www.lobstack.ai/gateway/routing) ·
[Connectors](https://www.lobstack.ai/connectors) ·
[Pricing](https://www.lobstack.ai/pricing) ·
[News](https://www.lobstack.ai/news) ·
[About](https://www.lobstack.ai/about)

</div>
