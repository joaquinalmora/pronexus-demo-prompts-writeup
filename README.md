# Links

- Write-up placeholder: [docs/architecture-and-reflection.md](docs/architecture-and-reflection.md)
- System prompt: [prompts/generate-system-prompt.md](prompts/generate-system-prompt.md)
- Brand voice prompt input: [prompts/brand-voice.md](prompts/brand-voice.md)
- Prompt assembly notes: [prompts/prompt-assembly-notes.md](prompts/prompt-assembly-notes.md)

## Notes

### Scoring
Each post includes a `qualityScore` from 1–5 and a `similarityScore` from 0–100. These are model-evaluated scores defined by the prompt rather than hardcoded formulas. The quality score is based on a rubric that asks the model to judge whether the post has the ingredients of a strong technical LinkedIn post: a concrete scenario, a clear failure/friction point, an adjustment or response, at least one grounded artifact such as a PR, deploy, repo, CI/CD workflow, or agent interaction, a hook with tension or specificity, and a tone that matches the selected voice. In practice, weaker posts are the ones that stay generic, abstract, or advice-heavy, while stronger posts feel more specific, experience-based, and operational. The similarity score is a rough originality check against the creator corpus, where 0 means highly distinct and 100 means very close in phrasing, structure, or ideas. 

### LinkedIn draft behavior
The LinkedIn action opens a LinkedIn share / draft-style flow using the generated post text, but it does not automatically publish anything to a LinkedIn account. The user still has to review the draft and manually post it inside LinkedIn. This works best when the user is already logged into LinkedIn, and because LinkedIn’s share behavior can vary, the app also copies the post text to the clipboard as a fallback.
