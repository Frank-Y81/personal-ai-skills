---
name: research
description: Structure complex research questions by decomposing them, evaluating evidence, and producing conclusions with explicit confidence levels.
version: 1.0.0
---

# Purpose

Help conduct structured research on complex questions. The skill focuses on decomposition, evidence evaluation, and transparent uncertainty — not on producing a single definitive answer.

# When To Use

- User asks a complex, multi-faceted question that requires analysis
- User provides materials and wants structured analysis
- Conflicting information exists and needs resolution
- A topic requires distinguishing facts from opinions
- User needs a structured summary of a research question

# Workflow

1. **Decompose the question**: Break the research question into sub-questions that can each be answered independently.
2. **Gather information**: Use available sources — user-provided materials, existing context, or external information. Do not assume any single source type is mandatory.
3. **Identify key findings**: Extract the most relevant facts, data points, and claims.
4. **Classify information**: Label each finding as:
   - **Fact**: Verifiable, evidence-backed statement
   - **Inference**: Logical conclusion drawn from facts
   - **Opinion**: Subjective judgment or perspective
5. **Identify conflicts**: Note where sources disagree or where evidence is contradictory.
6. **Evaluate evidence**: Assess the quality, recency, and reliability of each source.
7. **Synthesize**: Combine findings into a coherent conclusion.
8. **Assign confidence**: Express confidence level explicitly (High / Medium / Low) and explain what would change it.

# Decision Rules

- Always decompose before answering. A single monolithic answer to a complex question is a failure mode.
- If information sources conflict, do not pick one silently — present the conflict and explain the discrepancy.
- If no reliable evidence is available for a sub-question, state that explicitly rather than guessing.
- Confidence must reflect the quality and consistency of evidence, not the user's expectations.
- Distinguish between "no evidence found" and "evidence of absence".
- When the user provides materials, prioritize those materials over assumptions about what external sources might say.

# Output Format

```
## Research Question
[Restated and decomposed]

### Sub-questions
1. [Sub-question 1]
2. [Sub-question 2]
...

## Key Findings
- [Finding 1] — [Fact/Inference/Opinion] — [Source]
- [Finding 2] — [Fact/Inference/Opinion] — [Source]
...

## Conflicting Information
- [Conflict description]: [Source A says X; Source B says Y]

## Confidence: High / Medium / Low
[Explanation of what drives this confidence level]

## Conclusion
[Synthesized answer with caveats]
```

# Constraints

- Do not present inferences as facts.
- Do not omit conflicting information to produce a cleaner conclusion.
- Do not assume internet access is available. Work with whatever information sources are provided or accessible.
- Do not assign High confidence to conclusions based on a single source.
- Keep the output structured but adapt depth to the complexity of the question — simple questions don't need all sections.
