# Prompt assembly notes

## Runtime prompt structure

The app assembles the final request in three layers:

1. **System prompt template**
   - sets the global quality bar
   - defines structure, hook, and anti-slop constraints
   - includes the realism and polish rules used for the final pass

2. **Voice-specific rules**
   - founder voice: first-person, lived-experience framing, concrete contextual cues
   - company voice: neutral, system-focused framing, observable workflow outcomes

3. **Runtime user prompt**
   - injects the chosen industry, topic focus, audience, and voice preset
   - injects the creator corpus, brand voice markdown, and sampled trend data
   - enforces an exact JSON response shape
   - adds post-level constraints for hook quality, structure variety, linting, and similarity control

## Key runtime constraints

- every post needs a concrete scenario, friction point, and adjustment
- every post needs at least one concrete artifact such as CI/CD, repos, PRs, deploys, agents, tests, or logs
- prompts explicitly ban generic advice and several weak reflective phrases
- posts must stay believable and avoid fabricated precise metrics
- each post includes two hook variants, post linting output, and a similarity score against the creator corpus

## Model configuration

- default model: `gpt-4o-mini`
- response format: `json_object`
- temperature: `0.8`

## Environment variables used by the app

```env
OPENAI_API_KEY=
OPENAI_MODEL=gpt-4o-mini
DISABLE_GENERATION=false
```

## Notes

- the private application repo contains the full implementation and API flow
- this public repo is intentionally limited to prompts and the accompanying write-up
