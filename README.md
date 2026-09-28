# ISYS 650 Trip Planning Agent

This public portfolio project is the home for a five-person ISYS 650 group project: an AI trip-planning agent that parses vacation requests, asks for missing critical details, researches bounded travel information, and produces a linked, color-coded day-by-day itinerary with continued revisions.

## Assignment and rubric scope

The draft targets the course assignment over the next few weeks by demonstrating a practical agent workflow: request parsing, clarification, bounded research, itinerary synthesis, critique, and follow-up revision. The design is intentionally a first pass and will be refined against the team's rubric and instructor expectations.

## Current status

**Working code-first demo.** [Wanderplan](https://isys650.10server.net/) starts with an empty calendar. Ask Wanderbot uses OpenRouter web search to draft an itinerary of 1–30 days from the traveler's dates and accepts continued revisions to the current plan; Reset demo clears the plan and chat. It is a rough planning demo, not a booking service. The old blank Langflow export in `flows/trip-agent.json` is historical, not the runtime.

## Prompting skill

Zack's first prompting checkpoint is documented in [`docs/prompting-checkpoint.md`](docs/prompting-checkpoint.md). Its reusable behavior is encoded in [`skills/plan-multi-city-trip/`](skills/plan-multi-city-trip/). The skill maintains evolving constraints, checks route feasibility, synthesizes timed itineraries, builds complete budgets and savings goals, and includes reservation and safety guidance.

## Travel research skill

`skills/travel-browser-research/` contains the first data-and-tooling checkpoint: a Browser Harness workflow for researching an already-defined trip. It discovers candidates, verifies prices and restrictions on primary sources, and returns structured, source-backed data for the itinerary agent.

The skill is a research workflow and is not yet wired into the deployed app. OpenRouter web search supplies discovery snippets instead; the app does not independently verify each result on a primary site. It does not book travel, enter credentials, or guarantee prices and availability.

Every push to `main` runs [tests and deploys](.github/workflows/deploy.yml) the Docker app on 10server.net. The server calls `deepseek/deepseek-v4.1-flash` through OpenRouter with high reasoning and its web-search plugin; no `max_tokens` value is set. The key lives only on the server. The public demo has no password or app-side request limit: anyone can spend the server's OpenRouter key. Use a dedicated spend-capped provider key before sharing broadly. Don't use it for bookings or trust changing prices without checking linked sources. Browser Harness is **not** yet connected to the deployed agent.

Run tests locally with `uv run --no-project python -m unittest discover -s tests`. Repository commit conventions are in [`AGENTS.md`](AGENTS.md).
