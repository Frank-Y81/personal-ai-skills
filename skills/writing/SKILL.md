---
name: writing
description: Handle writing and rewriting tasks by analyzing goal, audience, and structure before producing or revising text.
version: 1.0.0
---

# Purpose

Help with writing and rewriting across formats (email, article, documentation, proposal, rewrite). The skill ensures that writing decisions are intentional — driven by purpose, audience, and structure — rather than generating text reflexively.

# When To Use

- User asks to write a new document (email, article, documentation, proposal, etc.)
- User asks to rewrite or improve existing text
- User has a writing goal but hasn't specified format or audience
- User needs help structuring a document

# Workflow

1. **Understand the goal**: What is the desired outcome of this writing? (Inform, persuade, request, document, etc.)
2. **Identify the audience**: Who will read this? What do they already know? What do they need to know?
3. **Determine structure**: Based on goal and audience, choose an appropriate structure (e.g., direct response, problem-solution, narrative, reference).
4. **Set the tone**: Professional, casual, formal, friendly — driven by audience and goal.
5. **Draft or revise**: Generate new text or modify existing text.
6. **Self-check**: Review against:
   - Does it achieve the goal?
   - Is it appropriate for the audience?
   - Is there unnecessary content?
   - Is the structure clear?
7. **Output**: Present the final text with optional brief notes on structural choices.

# Decision Rules

- For simple tasks (e.g., "rewrite this sentence more concisely"), skip the full workflow. Go straight to revision.
- If the user provides existing text, revise in place rather than rewriting from scratch — unless the structure is fundamentally wrong.
- If goal or audience is ambiguous, make a reasonable assumption and state it. Do not block on asking unless the ambiguity is critical.
- Do not add sections the user didn't ask for (e.g., don't add a TL;DR unless requested).
- Match the user's language. If they write in Chinese, respond in Chinese. If English, respond in English.
- Prefer clarity over style. Avoid jargon unless the audience expects it.
- When rewriting, preserve the user's intent — do not silently change the meaning.

# Output Format

```
[Drafted or revised text]

---
*Notes: [Optional — brief explanation of key structural or tonal decisions, only if non-obvious]*
```

# Constraints

- Do not over-structure simple writing. A one-paragraph email doesn't need a table of contents.
- Do not change the user's language or add translations unless asked.
- Do not add disclaimers, legal notices, or AI-generated content labels unless the user requests them.
- Do not pad the output with filler to meet a perceived length expectation.
