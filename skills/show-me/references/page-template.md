# Page template

Copy the skeleton, fill it from the model built in step 2, and delete every panel that has nothing to say. A small change gets the conclusion plus two or three panels; a large one gets five or six. The draft language is in `ARCHIFY/references/explainer-authoring.md` (the archify skill folder; see SKILL.md).

## Skeleton

````md
# <What the change does, as a plain title> {#<slug>}

<The idea in one or two sentences, with the key move in **bold**.>

- <Why: the problem it solves.>[](source:pr)
- <How: the core mechanism.>
- <What the reader should weigh in on first.>

@answer scope="<owner/repo>#<n> · head <short sha> · <files> files, +<add> −<del> · from the diff and description"
@meta locale=en
@source pr title="<owner/repo>#<n>: <PR title>" url=<PR url>
@source <id> title="<path>" url=https://github.com/<owner>/<repo>/blob/<head sha>/<path>#L<start>-L<end>

## What problem does it solve? {#problem}

<Two or three sentences: what broke or was missing, and who noticed. Use @facts for a few labelled facts such as the ticket, the symptom and the affected surface.>

## How does it work after this change? {#flow}

@sequence id=<content-name> title="<flow name>" changes="<edge-id>:added,<actor-id>:modified"
| actor ui | <label> | frontend |
| actor api | <label> | backend |
| actor db | <label> | database |
| ui | api | <request> |
| api | db | <query> |
| db | api | <result> | return |

@steps id=<content-name>-steps
| s1 | <node label> | <what happens there and why it matters> | <diagram id> | <node id> |

## What changes in the code? {#shape}

@tree id=<content-name> title="Touched modules" changes="<node-id>:added,<node-id>:modified"
| root | <repo> | - |
| <id> | <dir or file> | root |

| Area | Role in the change |
| --- | --- |
| `<path>` | <one line>[](source:<id>) |

## What data or state changes? {#data}

<Only when the change adds or alters stored data, config, flags or a contract. An @erd, a before/after table of fields, or a @diff of the struct or schema.>

## How does it ship? {#rollout}

<Only when deploy order, flags, migrations or backfills matter. @steps in order, with what breaks if the order is reversed.>

## Where is your feedback most useful? {#feedback}

- [ ] <Decision: what the author chose, the alternative, and the trade-off.>[](source:<id>)
- [ ] <Open question: the case the change does not cover.>

@callout level=note title="Not shown"
| <Tests, generated files and areas skipped.> |
````

## Choosing each panel's form

| The change is about | Draw |
|---|---|
| Messages between services, a request path, an API contract | `@sequence`, marking new messages `added` |
| A process with branches: a job, a state machine, a retry path | `@workflow` with decision nodes ending in `?` |
| A chain of checks or guards, each able to reject | `@workflow` drawing only the passing path, with the diagram title saying what a failure returns; the matching `@steps` give each rejection. Several edges into one shared error node fail Archify's crossing checks. |
| Which components exist and how they connect | `@architecture` |
| Where code moved or which modules it touches | `@tree` with `changes` |
| Tables, columns, keys | `@erd` |
| One function's logic | a plain ```` ```diff ```` or ```` ```text ```` fence with pseudocode |
| Several options the author weighed | a Markdown comparison table with `{good:…}` / `{caution:…}` cells |

## Marking changes

Any compact diagram takes `changes="<target>:added|removed|modified,..."`, which highlights those parts. A target is a node or actor ID, or an edge ID. Compact edges and messages get the ID `<from>-to-<to>-<n>`, where `<n>` counts repeats of the same pair from 1, in row order. Mark only what the change touches; the unmarked parts are the existing shape the reader already knows.

A `removed` target must still be drawn. When the point is that something goes away, draw the before state with the removed parts marked, or show a before/after pair of diagrams.

## Citations

For a PR, cite code with GitHub blob URLs pinned to the head SHA and a line range, as in the skeleton; this needs no local checkout. Use `@code` with `--repo-root` only when the head commit exists in a local clone.
