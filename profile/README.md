# Puxti Labs

**Puxti** *(POOKH-tee)* — from *puxtiri* (*pux-TÍ-ri*), Aymara for "the murmur of water."


---

## What we're building

A tool called **Puxti** that propagates schema and semantic changes across
a data stack *safely*, as small, reviewable pull requests, by grounding
every change in a Knowledge Graph of producers, dbt models, downstream
consumers, and the semantic links between them.

Rename a column. Redefine what *active user* means. Puxti finds everywhere
it matters and opens PRs in the right repos, so the change becomes a
conversation instead of a surprise.

With `puxti mcp serve`, the same Knowledge Graph is available as an MCP
server — so AI coding agents like Claude Code or Cursor can query blast
radius before they touch anything.

## Try it

Open source. Apache 2.0. Bring your own LLM key for semantic reasoning — Anthropic by default; OpenAI, Mistral, Gemini, AWS Bedrock, local Ollama, and more.

```bash
pip install puxti
puxti scan          # populate the Knowledge Graph from your dbt project
puxti describe      # see what Puxti knows about your stack
puxti impact model.jaffle_shop.orders  # blast radius before you change anything
puxti mcp serve     # expose the graph as an MCP server for AI coding agents
```

- 📦 [pypi.org/project/puxti](https://pypi.org/project/puxti/)
- 🔧 [github.com/puxti-labs/puxti](https://github.com/puxti-labs/puxti)


---

## Why this exists

You rename a column in a dbt model. What breaks?

Probably three downstream models, an ML model that does a manual `SELECT`,
two Looker explores, a Superset Finance dashboard nobody remembered existed, and the
data dictionary in Notion that was already six months out of date.

Finding all of that is a Monday-morning ritual for most data teams. Fixing
it means opening four tools, making four edits, and hoping the reviewers on
each side have the context to know whether the change is correct.

Modern data stacks are held together by implicit knowledge: who uses what,
what a column *means*, which dashboard still matters. That knowledge lives
in people's heads, Slack threads, and the grep history of whoever's been
there longest. When it walks out the door, things break quietly.

Puxti tries to make that knowledge explicit, queryable, and, when things
change, actionable.

---

## The idea

Two primitives, one substrate.

**The substrate** is a **Knowledge Graph**. Puxti scans your stack and
builds a map: producers, dbt entities, orchestration references,
dashboards, docs, and the semantic links between them. This is what makes
"safe" possible — propagation without a graph is just find-and-replace
with more steps.

**The two primitives** are the two kinds of change that actually happen:

- **`capture`** — a *schema* change. A column rename, a type change, a
  table split. Structural.
- **`redefine`** — a *semantic* change. The definition of *active user*
  shifts from "logged in this week" to "opened the app this week." Same
  column, different meaning.

Each lands as a reviewable PR in the right place. Small, reversible,
visible. Changes become conversations instead of silent rewrites or
Monday morning archaeology.

---

## Why the name

I have a soft spot for words from ancient languages that describe things
other languages can't quite reach, the way Japanese has *ikigai*, or
German has *Waldeinsamkeit*.

Puxtiri is an Aymara word meaning "the murmur of water", the sound of a
river moving through a landscape. I liked it because it captures something
about how data should actually behave: flowing continuously, audibly
enough that you notice when it changes.
Puxti is the short form—a small homage to a language that describes moving water better than most.

Most data tools are named like medications or industrial equipment. 
This one is named after the sound a river makes. That’s on purpose.

---

## Why now

Execution barriers in software are collapsing. A single engineer with the
right tools can ship in a week what used to take a team a quarter. That
shifts where the hard work is, away from implementation, toward knowing
what's worth building and making it legible to the humans who have to
review it.

Puxti is a small bet in that direction: a tool that doesn't replace data
engineers, but removes the part of the job that's archaeology so they can
spend more time on the part that's design.

---

## Status

- **`puxti`** — v0.10.0 on [PyPI](https://pypi.org/project/puxti/).
  Open source under Apache 2.0. No Docker, no external services — graph lives locally in SQLite.
  Provider-agnostic BYOK: bring a key from Anthropic (default), OpenAI, Mistral, GLM,
  DeepSeek, Groq, OpenRouter, Gemini, AWS Bedrock, or run local Ollama with no key at all.
- Core commands: `scan`, `describe`, `link`, `capture`, `redefine`, `correct`, `purge`,
  `config`, `health`, `impact`, `telemetry`, `mcp`.
- **MCP server** — `puxti mcp serve` exposes four read-only tools to coding agents (Claude Code, Cursor).
  Query the Knowledge Graph without leaving your IDE.

## Repositories

- [**puxti**](https://github.com/puxti-labs/puxti) — the CLI
- [**puxti-demo-project**](https://github.com/puxti-labs/puxti-demo-project) — sample dbt project for trying Puxti
- [**airflow-demo-project**](https://github.com/puxti-labs/airflow-demo-project) — sample Airflow project showing cross-system links

If you run a data team and this resonates, especially if you've lived
the "what breaks when I rename this column" question, I would love to hear
what your version of the problem looks like.
- Reach out: 📫 [hello at getpuxti.com](mailto:hello@getpuxti.com)

---

## Who's behind it

Built by [Sebastián Villarroel](https://github.com/sebastianvillarroel) —
Fifteen years across insurance, fintech, telco, and startups taught me what data teams need to move fast without breaking downstream. Puxti is some of that, in a tool.