# How we work

This applies to every repository in Lobstack-ai that doesn't have its own
CONTRIBUTING file. Repos with one (like the app's) add their own rules on top.

## Everything starts as a ticket

Open an issue and pick a form:

- **Bug** — something is broken.
- **Feature** — something new, or a change to how something works.
- **Task** — everything else: chores, cleanups, release steps, docs.

A quick one-line issue is fine too. It lands in **Inbox** and gets sorted there.

## The board

All tickets from every repo land on one Kanban board, the
**Lobstack Engineering** project. Each ticket moves left to right:

| Column | Means |
|---|---|
| **Inbox** | New, not looked at yet. |
| **Ready** | Understood and worth doing. Has a priority and a size. |
| **In progress** | Someone is working on it now. It has an assignee. |
| **In review** | A pull request is open. |
| **Blocked** | Waiting on something outside our control. Say what in a comment. |
| **Done** | Merged or finished. Closes automatically when the PR merges. |

**Priority**

- **P0** — people can't use Lobstack, or money or data is at risk. Drop everything.
- **P1** — this week.
- **P2** — soon. Most tickets.
- **P3** — nice to have.

**Size**

- **XS** — under an hour.
- **S** — a few hours.
- **M** — about a day.
- **L** — a few days.
- **XL** — too big; split it first.

## Picking up work

1. Take the top ticket in **Ready** that fits, assign yourself, and move it to **In progress**.
2. Keep two tickets or fewer in progress at a time each. Finishing beats starting.
3. Branch as `<kind>/<issue number>-<short-name>`, for example `bug/412-signin-loop`.
4. Open a pull request with `Closes #<number>` in the description. The ticket moves to
   **In review** and then **Done** on merge.
5. The other engineer reviews. Small PRs get reviewed faster.

## Once a week

Empty the **Inbox**: for each ticket, give it a priority and a size and move it to
**Ready**, or close it with a one-line reason.

## Shipping

- **Website, API and Console** (`lobstack`): merging to `main` deploys to production, so
  everything goes through a pull request.
- **App** (`lob-bot`): a release happens only when a version tag is pushed. Merging to
  `main` doesn't release anything.
- **npm packages** (`lobstack-gateway`, `lobstack-mcp`, `lobstack-cli`): publish by pushing a
  `v*` tag. The token lives only in the repository's Actions secrets.

## Security

Don't open a public issue for a security problem. Email hello@lobstack.ai instead
(see https://www.lobstack.ai/docs/security).
