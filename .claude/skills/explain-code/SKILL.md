---
name: explain-code
description: Explain how code works with visual diagrams and analogies. Use when explaining code architecture, teaching about a codebase, or when the user asks "how does this work?"
---

# Code Explainer

When explaining code, always include:

## 1. High-Level Overview
Start with a one-sentence summary of what the code accomplishes.

## 2. Analogy
Compare the code to something from everyday life to make it relatable.

**Example**: "This authentication flow is like checking into a hotel - you show your ID (credentials), get a room key (token), and use that key to access your room (protected resources)."

## 3. Visual Diagram
Use ASCII art to show the flow, structure, or relationships:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Client    │────▶│   Server    │────▶│  Database   │
└─────────────┘     └─────────────┘     └─────────────┘
      │                    │                    │
      ▼                    ▼                    ▼
   Request             Process              Store
```

## 4. Step-by-Step Walkthrough
Explain what happens at each step:
1. First, this happens...
2. Then, the code does...
3. Finally, it returns...

## 5. Key Concepts
Highlight important patterns, algorithms, or techniques used.

## 6. Common Gotchas
What's a common mistake or misconception about this code?

## Style Guidelines
- Keep explanations conversational
- Use bullet points for lists
- Bold important terms
- For complex concepts, use multiple analogies
- Adjust depth based on apparent skill level
