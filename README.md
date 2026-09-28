# Tyrell Engagement — A Worked Example

## What this is

This is a made-up example. It is meant to show hiring teams how I approach a problem across design, product, and engineering: how I read the material, find the real constraints, pick a direction, and build something that runs.

Every company, person, claim, and number in it is fictional. **Tyrell Corporation** is the client, a third-party claims administrator processing ~400K commercial auto claims a year. **Acme** is the AI partner it has hired. The repo is Acme's engagement workspace, at the end of week 1 of a two-week discovery inside a six-month, $5M engagement to ship Tyrell's first production AI capability.

## The scenario

Tyrell signed a statement of work against four goals:

| Goal | Today | Target |
|---|---|---|
| Cost to serve | $430–$650 per claim | −25% blended |
| Cycle time | 68h average | <24h for simple claims |
| Human review rate | 45% of claims flagged | <20% |
| Customer satisfaction | 3.2 | >4.0 |

The hard parts are the constraints, not the model:

- **AI cannot decide a claim.** Every denial is a human decision. Several states require human review above $10K, and every AI-assisted decision needs a seven-year audit record.
- **The system of record is a legacy vendor platform.** It has a REST API for reads, SOAP for writes, an unreliable webhook, and no API for decisions at all.
- **Two earlier AI attempts failed.** A 2021 scoring model shipped, drifted, and lost the adjusters' trust. A recent RAG project never converged.
- **The data has known problems.** OCR runs at ~78% on faxes, an EDI parser silently drops ~1 in 8 submissions, and labels disagree with the stated rules.

The task: by the end of week 1, form a point of view on what to build first and why, and back it with a working demo.

## What's here

| Path | What it holds |
|---|---|
| `AGENTS.md` (also `CLAUDE.md`) | Engagement context: who's who, goals, systems, constraints |
| `docs/project/` | The signed SOW and pre-engagement research notes |
| `memory/calltranscripts/` | The three week-1 discovery calls: kickoff, operations walkthrough, systems |
| `memory/decisions.md` | Decisions of record, with reasoning |
| `reference/` | What the client handed over: claims extract, data dictionary, analytics memo |
| `sample_claims/` | Three representative claim files (intake, fax, EDI, photos, call excerpts) |
| `analysis/` | Scripts that check the client's claims against their own data |
| `docs/discovery/` | Open questions, each with why it matters and its source |
| `docs/architecture/` | How the proposed system fits the client's estate |
| `docs/presentation/` | Presentation draft and side-panel spec |
| `demo/` | The running demo: routing pipeline, admin monitor, mock vendor screen, browser side panel |

## Where to start

1. `AGENTS.md`, for the cast and the constraints.
2. The three transcripts in `memory/calltranscripts/`. Most of the reasoning is grounded there.
3. `docs/discovery/open_questions.md`, for what the data does and doesn't support.
4. `demo/README.md`, to run the demo (`just dev`, then <http://localhost:8000>).

## How it was built

AI tools were used throughout: for data analysis, drafting, and building the demo. The rule I held myself to is that every element has to be defensible on its own. Every finding cites a source file and line, and every pushback on the client's numbers comes with a script that reproduces it.
