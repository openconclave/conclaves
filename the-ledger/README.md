# The Ledger

A conclave for people about to make an irreversible decision — quit, leave, sign, commit. Two agents build opposing lists; a code node mechanically detects items that describe the same underlying pattern. You read the highlighted ledger and decide.

## What it does

You open a chat trigger and describe, in one paragraph, the decision you're facing and the context around it: what you've already put in, and what continues to be unavailable if nothing changes.

Then:

1. A **Sunk Cost agent** and an **Opportunity Cost agent** take turns (strict alternation, 6 rounds) — each adds 2-4 items per turn in its own category, with evidence drawn from your context.
2. A **Moderator** (Claude Haiku) enforces the alternation.
3. A **Python code node** embeds every item via Ollama's `nomic-embed-text`, computes pairwise cosine similarity between sides, and flags pairs above threshold 0.72 as the **same underlying pattern, stated from two directions**. Greedy assignment so each item appears in at most one pair.
4. The code node writes three artifacts:
   - A plain-text ledger (delivered via the channel output)
   - A heatmap PNG (`ledger-<runId>/heatmap.png`)
   - A full HTML ledger with explanations (`ledger-<runId>/ledger.html`)

## Why it works

A single LLM asked to evaluate a decision tends to hedge or produce the safe both-sides bullet list. The Ledger does something a single LLM structurally can't: it produces two independent lists under constrained prompts, then runs a *mechanical* operation (cosine similarity of embeddings) on them. The overlaps that emerge are patterns neither agent wrote — they're artifacts of comparing the two lists.

When an item appears on both sides, it means the force driving what you're trying to protect is the same force foreclosing what's becoming unavailable. That's the moment of recognition the conclave is designed to produce. The user does the final interpretive work.

## Topology

```
Chat trigger (user describes the decision)
        │
        ▼
   Discussion (6 rounds, strict alternation)
   ├── Sunk Cost agent       (list-only, 2-4 items/turn)
   ├── Opportunity Cost agent (list-only, 2-4 items/turn)
   └── Moderator (Haiku)      (enforces alternation)
        │ full transcript
        ▼
   Code node (Python)
   └── Extract items → embed via Ollama → cosine pairwise
                    → greedy dedup → render heatmap + HTML
        │
        ▼
   Claude Code channel output (plain-text ledger + file paths)
```

## Requirements

- **OpenConclave** — https://github.com/openconclave/oc
- **Anthropic API key** — for the three Claude agents
- **Ollama** — for embeddings: `ollama pull nomic-embed-text`
- **Python** — for the code node (auto-installs `numpy`, `pandas`, `matplotlib`, `seaborn` on first run)

## How to import

```
Conclaves → ⬇ Import → paste this URL or drop conclave.json:
https://raw.githubusercontent.com/openconclave/conclaves/main/the-ledger/conclave.json
```

Then start the chat trigger and describe a decision you're actually facing. First run will pip-install plotting deps (30-60s). Subsequent runs are faster.

## Notes on reading the output

1. **Heatmap first (30 seconds).** Rows are sunk-cost items, columns are opportunity-cost items. Dark-red cells with a red border are the machine's same-pattern flags.
2. **Highlighted rows in the two-column ledger (2 minutes).** Items marked ⚠ appeared in a flagged pair — read those first.
3. **Pair cards (5 minutes, slowly).** Each card is one pattern, stated once as what you're protecting and once as what's being foreclosed. Read each as a loop. That's the insight.

## License

MIT.
