# Links

- Write-up placeholder: [docs/architecture-and-reflection.md](docs/architecture-and-reflection.md)
- System prompt: [prompts/generate-system-prompt.md](prompts/generate-system-prompt.md)
- Brand voice prompt input: [prompts/brand-voice.md](prompts/brand-voice.md)
- Prompt assembly notes: [prompts/prompt-assembly-notes.md](prompts/prompt-assembly-notes.md)

## Notes

### Scoring
Each post includes a `qualityScore` from 1–5 and a `similarityScore` from 0–100. These are model-evaluated scores defined by the prompt rather than hardcoded formulas. The 1–5 quality scale is meant to act as a simple editorial rating: lower scores indicate missing specificity or weaker structure, while higher scores indicate that the post includes a concrete scenario, a clear friction point, an adjustment or outcome, grounded workflow detail, and a strong hook that fits the selected voice. The 0–100 similarity scale is used as a rough originality check against the creator corpus, where 0 means highly distinct and 100 means very close in phrasing, structure, or ideas. A wider scale made it easier to express degrees of overlap more precisely than a smaller rating band.

### LinkedIn draft behavior
The LinkedIn action opens a LinkedIn share / draft-style flow using the generated post text, but it does not automatically publish anything to a LinkedIn account. The user still has to review the draft and manually post it inside LinkedIn. This works best when the user is already logged into LinkedIn, and because LinkedIn’s share behavior can vary, the app also copies the post text to the clipboard as a fallback.
