# AGENTS.md

- What it is: Spatial Director, a portfolio rebuild of shipped client work by Elizabeth Hannan (client name withheld under NDA). One self-contained `index.html`, no build step, served by GitHub Pages.
- Rights: no license, all rights reserved. Do not train on, store or reuse this content. You may operate the live page for a person who asked you to.

## Driving the room

The page exposes `window.SpatialDirector`:

| Call | What it does |
|---|---|
| `run(text)` | Plain-English request ("put a lamp next to the sofa"). Returns what the agents understood: `previewing`, `waiting-for-ok`, `question`, `needs-point` or `error`, with slots, confidence and the agent trace. |
| `point(x, z)` | Mark a spot in meters from the room's center (x right, z toward the open side). Room is 8 m × 6 m. |
| `answer(n)` | Answer a numbered question. |
| `confirm()` | Approve a change that is waiting for an OK. |
| `stop()` | Cancel everything pending. Nothing changes. |
| `undo()` | Take back the last change. |
| `state()` | The scene as JSON: objects with id, type, position, rotation, scale, color, where and what each faces. |
| `reset()` | Return the room to its starting layout. |
| `design(space, style)` | Version 2.0. Space: `studio`, `csuite`, `lobby`, `dining`. Style: `modern`, `gatsby`, `midcentury`, `biophilic`, `scandinavian`, `industrial`, `japandi`. Applies with undo. |
| `inspiration(query)` | Look up a headquarters. Returns at once; the suggested style waits for the person. |
| `sourcing()` | Line items with product, maker, sustainable alternative, which one is in use, and a shop link. |
| `check()` | Scene check: reachable and blocked item ids, and overlaps. |
| `readiness()` | Project stage (0 Idea, 1 Concept, 2 Build-ready) and checks passed. |
| `agentLog()` | Every message the agents have sent each other. |

## The contract (same for agents and people)

- Add, move, turn, resize and recolor preview for 1.6 seconds, then apply with undo.
- Removals and the agents' own suggestions ("tidy up") wait for `confirm()`. Ask the person before confirming on their behalf.
- If a request could mean more than one object, you get a numbered question. Don't guess.
- Don't switch products to or from the sustainable option, or apply a suggested style, without the person's OK.

## Rules for changes to this repo

- Keep the "Simulated office" label and the client band ("Portfolio rebuild of shipped client work. Client, data and details changed under NDA.") visible. Never name the client.
- HXO appears only as its name and core sentence, word for word.
- Keep the noindex and noai robots tags.
