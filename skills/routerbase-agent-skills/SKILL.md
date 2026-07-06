---
name: routerbase-agent-skills
description: Use routerbase as an OpenAI-compatible gateway for API integration, model routing, and media generation workflows.
---

# RouterBase Agent Skills

Use [routerbase](https://routerbase.com/) as an OpenAI-compatible gateway for GPT, Claude, Gemini, image, video, audio, and other model workflows. This skill helps agents produce practical integration guidance without exposing API keys or private user data.

Full source package: https://github.com/zenlee123/routerbase-agent-skills

## When To Use

- Migrating OpenAI-compatible SDK calls to RouterBase.
- Setting the base URL to `https://routerbase.com/v1`.
- Choosing RouterBase model IDs for chat, vision, image, video, audio, or embeddings workloads.
- Designing model fallback plans across providers.
- Building media generation flows that handle synchronous images and asynchronous video or audio tasks.
- Documenting RouterBase setup for Python, JavaScript, curl, LangChain, LlamaIndex, Vercel AI SDK, Cursor, Continue, or other compatible clients.

## API Integration Pattern

1. Keep credentials server-side in `ROUTERBASE_API_KEY`.
2. Reuse the user's OpenAI-compatible client when possible.
3. Change the base URL to `https://routerbase.com/v1`.
4. Use a RouterBase model ID for the target task.
5. Add a minimal smoke test only when credentials are available and the user expects a live API call.

```js
import OpenAI from "openai";

const client = new OpenAI({
  apiKey: process.env.ROUTERBASE_API_KEY,
  baseURL: "https://routerbase.com/v1",
});

const response = await client.chat.completions.create({
  model: "google/gemini-2.5-flash",
  messages: [{ role: "user", content: "Write one sentence about model routing." }],
});

console.log(response.choices[0].message.content);
```

## Routing Guidance

- Classify the modality first: chat, image, video, audio, embeddings, or mixed.
- Identify hard constraints: quality, latency, price, context length, tool calling, vision, JSON mode, and fallback tolerance.
- Query the live RouterBase catalog when credentials are available.
- Recommend one primary model and one or two fallback models.
- Treat model availability and prices as changeable; tell the user to verify before production.

## Media Guidance

- Use `POST https://routerbase.com/v1/images/generations` for image generation.
- Use `POST https://routerbase.com/v1/videos/generations` for video generation.
- Use `POST https://routerbase.com/v1/audio/speech` or `POST https://routerbase.com/v1/audio/generations` for audio workflows.
- Poll asynchronous video or audio tasks with backoff unless the application already has a durable callback URL.
- Persist generated media promptly because hosted media can have limited retention.

## Guardrails

- Never paste, log, or commit real API keys.
- Use placeholders such as `ROUTERBASE_API_KEY` or `sk-rb-...` in examples.
- Never put RouterBase keys in browser, mobile, or public repository code.
- Validate model-specific parameters before presenting production code.
- Avoid sending private prompts, media URLs, or user data into logs.
