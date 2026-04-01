# Architecture and Reflection

## System overview

I built this as a simple Next.js app centered around a single generate flow for LinkedIn posts about AI coding workflows. From the UI, the user picks a voice preset and triggers generation, which sends a request to `/api/generate`. On the backend, I load local prompt and seed data files, assemble a layered prompt, and send one structured request to OpenAI (GPT-4o). The model returns a strict JSON response with a style guide, trend brief, and a batch of posts. Before anything hits the UI, I validate the schema and run basic guardrails like prompt-leak checks. The frontend then just renders everything in a way that makes it easy to review rather than publish immediately.

## Data sources and ingestion approach

For this demo, I intentionally kept all inputs local instead of building a live ingestion pipeline. The creator corpus (`data/creators.json`) holds example posts along with tone and structure patterns, which I use to guide style without copying content. The trend inputs (`data/trends_seed.json`) simulate current signals in AI coding workflows and feed into the generated trend brief. Brand voice lives in `data/brand_voice.md` and defines how things should sound.

Keeping everything local made the system much more predictable and easier to debug. I didn’t have to deal with flaky APIs or inconsistent data. The tradeoff is that the trends are not truly real-time, so the system feels more like a controlled simulation than a live content engine.

## Prompting strategy

I approached prompting as a layered system rather than a single instruction. The system prompt sets the quality bar and pushes the model toward specific, grounded outputs while blocking generic phrasing. On top of that, I added voice rules so the same pipeline can produce either founder-style posts, which feel more personal and experience-driven, or company-style posts, which are more neutral and system-focused.

At runtime, I inject the creator corpus, trend inputs, and brand voice into the prompt, along with a strict JSON schema. I also ask the model to return scoring, linting, and similarity signals alongside the posts. Returning everything as structured JSON made a big difference. It keeps the UI deterministic and makes it easier to reason about failures, since I can validate the shape before rendering anything.

## Why these design choices

I chose local seeded data mainly for reliability. It made the system easier to reason about and removed a lot of failure points, but it does limit realism. The single generation call was another tradeoff. It keeps the architecture simple and ensures all outputs are consistent with each other, but it increases latency and means that if something goes wrong, the whole request fails.

Using JSON output was one of the more practical decisions. It made validation straightforward and allowed me to expose internal signals like quality scores and lint warnings without extra parsing. For evaluation, I relied on the model itself to score quality and similarity. That was fast to implement and good enough for a demo, but it is not something I would fully trust in a production system.

The voice presets were added to show that the system can shift tone without changing the pipeline. That worked, but it did add complexity to the prompt and made it more sensitive to small changes.

## Reflection and scaling

Right now the system is static and built around a single generation call, so scaling it would mean breaking that apart. The first step would be replacing the local seed data with a real ingestion pipeline that pulls from sources like Hacker News, Reddit, or product changelogs, then normalizes and stores that data.

I would also split generation into stages, like style extraction, trend synthesis, post generation, and evaluation. That would make it possible to cache intermediate outputs and reduce repeated work. Evaluation would need to move beyond model self-scoring, likely using embeddings or more explicit heuristics for similarity and quality checks.

On the cost side, caching things like style guides and trend briefs would help, along with using smaller models for parts of the pipeline. For scalability, I would move away from a single synchronous request and use async jobs and queues so batches can be generated in parallel.

There is also no feedback loop right now. Ideally, accepted or edited posts, or even performance signals like impressions and engagement, would feed back into the system to improve future outputs.

For the LinkedIn integration, the current approach just opens a prefilled draft, which keeps things simple and safe. A next step would be adding a second option using OAuth to post directly to LinkedIn. That would require a proper edit step in the UI so users can review and modify the content before it is published to their account.
