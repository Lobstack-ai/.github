## Lobstack

**One OpenAI-compatible key. Every model. A receipt on every call. An agent that
waits for you before it changes anything.**

Lobstack is a metered gateway for model calls. One key reaches 26 models across
9 providers — Anthropic, OpenAI, Google, xAI, DeepSeek, Mistral, Groq, Qwen and
Moonshot — through an OpenAI-compatible endpoint. Name a model and you get it.
Ask for `auto` and the request is scored for complexity and served by the
cheapest model that can answer it, never above the ceiling your plan sets.

Either way, the response tells you what happened: which model served it, what it
cost, and what the comparison was measured against.

---

### The receipt

Most gateways route. The question worth asking is what comes back when the
router picks for you. On Lobstack it is this, on every response — headers on a
buffered call, and on the final SSE frame under `x_lobstack` when you stream:

```json
{
  "request_id": "2f1c…",
  "served_model": "gemini-3.8-flash",
  "requested_model": "claude-opus-5",
  "routed": true,
  "cost_usd": 0.003281,
  "savings_usd": 0.018594,
  "priced": true,
  "baseline_model": "claude-opus-5",
  "baseline_reason": "named",
  "baseline_cost_usd": 0.021875
}
```

Two rules hold that together, and they are the reason the number is worth
reading.

**`cost_usd` is `null`, never `0`, when the price is unknown.** A model the
registry does not carry, or a stream that ended before it could be metered,
records an absence. Zero is a claim — that the call was free — and rendering a
missing price as free writes off real spend. `priced` says which case you are
in.

**A saving never travels without the reason it exists.** `baseline_reason` is
`named` when you asked for a specific model and the router served something
cheaper: the comparison is against your own request. It is `plan_ceiling` when
you sent `auto`, where the comparison is the most expensive model your plan
could have reached — a model nobody asked for, and the most flattering number
available to us, which is exactly why it is labelled rather than blended in.
Where there is no honest comparison, no saving is reported at all.

The full contract — every header, the baseline rule, what a ledger row stores —
is at [docs/gateway/metering](https://www.lobstack.ai/docs/gateway/metering).

---

### Products

**[Gateway](https://www.lobstack.ai/gateway)** — the API. `POST` to
`https://www.lobstack.ai/api/gateway/v1/chat/completions` with one key.
OpenAI-shaped requests and responses, streaming and tool calls included, so an
existing SDK needs a base URL changed and nothing else. Managed mode runs on our
provider keys; BYOK runs on yours, through the same endpoint and the same
metering. For anyone who is paying for model calls and cannot currently say
which feature, customer or prompt the bill came from.

**[Console](https://www.lobstack.ai/console)** — the surface over what the
Gateway did. Every request that reached the API, including the ones that failed
before a token existed: counts, error class, p50/p95/p99 latency, and cost
priced at the moment it was spent and frozen there, grouped by model, by key or
by agent. Managed and BYOK spend are counted apart, because only one of them is
yours to pay us for. For the person who has to attribute the spend and explain
the failures.

**[Lob Bot](https://www.lobstack.ai/lob-bot)** — a desktop application where
bots do real work on your own machine. The rule the product is built on is that
a step which only reads runs straight through, and a step that changes something
stops and shows you the exact call before it happens. It runs against your own
files and credentials, with no Lob Bot account and nothing phoning home. It is
prerelease: there is no published installer, the builds are not code-signed or
notarised, and the source is not public. For people who want an agent they can
leave running rather than one they have to watch.

---

### Open source

Three repositories are public, all MIT.

**[lobstack-cli](https://github.com/Lobstack-ai/lobstack-cli)** — the Gateway
from your terminal. `chat` streams an answer to stdout and the receipt to
stderr, so redirecting to a file gives you the answer alone. `models` prints
what the Gateway will serve and at what price, `spend` prints what you have
spent, and `proxy` binds a local OpenAI-compatible endpoint so Cursor, Aider or
Continue route and meter through Lobstack without ever holding your key. There
is a terminal UI with the price of the last call pinned under the conversation.
Zero dependencies. npm package `lobstack`.

**[lobstack-mcp](https://github.com/Lobstack-ai/lobstack-mcp)** — an MCP server,
for Claude Desktop, Claude Code, Cursor, Zed or anything else that speaks the
protocol over stdio. Four tools: `lobstack_route_preview`, `lobstack_models`,
`lobstack_chat` and `lobstack_spend`. Route preview needs no credential at all,
so an agent can ask where a prompt would go and what it would cost before you
have an account. npm package `@lobstack-ai/mcp`.

**[lobstack-gateway](https://github.com/Lobstack-ai/lobstack-gateway)** — a
typed SDK and, more usefully, the published contract it speaks: `spec/openapi.yaml`
for the endpoints, their headers and their error classes, and
`spec/x_lobstack.schema.json` for the receipt itself. A receipt nobody can
validate is a quirk; a receipt with a schema is a contract. npm package
`@lobstack-ai/gateway`.

**All three are on npm.** `lobstack` is at `0.1.1`, `@lobstack-ai/mcp` and
`@lobstack-ai/gateway` at `0.1.0`. The CLI skips `0.1.0` because that version was
published and unpublished on 2026-09-11 and npm keeps a permanent tombstone for
an unpublished version, so `0.1.1` is the lowest number that can exist under the
name. The site reads the registry state out of one module rather than asserting
it here, and says which day it was last checked:
[lobstack.ai/docs/cli](https://www.lobstack.ai/docs/cli).

---

### Quickstart

The API is live. Mint a key in the Console, then:

```bash
curl https://www.lobstack.ai/api/gateway/v1/chat/completions \
  -H "Authorization: Bearer $LOBSTACK_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model":"auto","messages":[{"role":"user","content":"Say hi"}]}' -i
```

The body is the OpenAI shape you already parse. The cost, the served model, the
baseline and its reason are in the `x-lobstack-*` response headers.

Pointing an existing client at it is a one-line change:

```ts
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: process.env.LOBSTACK_API_KEY,
  baseURL: "https://www.lobstack.ai/api/gateway/v1",
});
```

[Full quickstart](https://www.lobstack.ai/docs/quickstart) ·
[CLI](https://www.lobstack.ai/docs/cli) ·
[MCP](https://www.lobstack.ai/docs/mcp)

---

### How it is priced

A plan includes **dollars of model spend**, not messages. A message is not a
unit of cost — it is anything from a forty-token ping to a 200k-token context
with a tool loop behind it — so selling one as if it were a fixed quantity
misprices both sides of the deal.

Managed traffic is charged at 1.25× the provider's own list price, and that
multiplier is on the receipt and in the ledger row. The spread is deliberately
modest: a customer who can compare our number against a public price list will
do exactly that. BYOK is metered by request count instead, because you pay your
own provider and there is no token cost of ours to meter.

There is a free plan with a dollar of included spend, a key, and the same
receipt on every call. Annual billing is 20% below monthly across the paid
plans. Current numbers are on [pricing](https://www.lobstack.ai/pricing).

---

### What is not claimed here

Lobstack is early, and the pages that would normally hide that instead say so.
The [status page](https://www.lobstack.ai/status) computes availability from
real request traffic rather than synthetic probes, and reports "no data" where
there is not enough of it to report anything else. The model catalogue carries
the date every price was last checked against the provider's own page, and
flags any rate that could not be confirmed. SOC 2 Type II controls are mapped
with audit-ready documentation; **no audit has been performed and the
certification is not claimed** — [security](https://www.lobstack.ai/docs/security)
states which controls run and which are written down and not deployed.

[Compare](https://www.lobstack.ai/compare) grades the competition on four
questions and does not put Lobstack in the table, because a vendor scoring
itself in its own matrix always wins and everyone reading knows it.

---

### More

[Website](https://www.lobstack.ai) ·
[Docs](https://www.lobstack.ai/docs) ·
[Gateway API](https://www.lobstack.ai/docs/gateway) ·
[Routing](https://www.lobstack.ai/gateway/routing) ·
[Connectors](https://www.lobstack.ai/connectors) ·
[Pricing](https://www.lobstack.ai/pricing) ·
[Status](https://www.lobstack.ai/status) ·
[News](https://www.lobstack.ai/news) ·
[About](https://www.lobstack.ai/about)

The connector catalogue is Lob Bot's, and it is on the site rather than in this
file, because a count typed into a README is a count that goes stale silently:
[lobstack.ai/connectors](https://www.lobstack.ai/connectors).

---

### Contact

Questions, bug reports and anything else: **hello@lobstack.ai**. Issues on the
three public repositories are read. If a Gateway call went wrong, include the
`x-lobstack-request-id` from the response — every request carries one, allocated
before anything can fail, so even a 401 comes back with an id worth quoting.
