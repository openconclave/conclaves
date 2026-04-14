# Starter Conclaves

Importable conclave definitions for [OpenConclave](https://github.com/openconclave/oc). Drop the `.json` file into your OC instance to try it out.

## How to import

1. Open your OC instance (default: `http://localhost:4000`)
2. Go to **Conclaves**
3. Click **⬇ Import**
4. Select the `conclave.json` file (or paste its URL)
5. Hit **Run**

Each conclave below lives in its own folder with a `conclave.json` (the definition) and a `README.md` (what it does and how to use it).

## Available

| Starter | What it does | Requires |
|---|---|---|
| **[The Ledger](./the-ledger)** | For people about to make an irreversible decision — quit, leave, sign, commit. Two agents build sunk-cost and opportunity-cost lists; a code node mechanically detects items that describe the same underlying pattern. You read the highlighted ledger and decide. | Anthropic API key, Ollama with `nomic-embed-text` |

## Coming soon

- **Code Review** — 5 specialists review your code in parallel. Findings get severity tags, line numbers, and proposed fixes. A knowledge base captures lessons so the next review is smarter.
- **Brainstorm** — Agents pitch ideas, a critic tears them apart, a moderator steers the debate. You get a structured verdict — not a list of bullet points.
- **Three Advisors** — Ask any question. Three agents answer independently, then a fourth merges their perspectives into one response.
- **Agent Mafia** — AI agents play Mafia against each other. You just watch.

Pull requests welcome.

## License

MIT — use, remix, ship.
