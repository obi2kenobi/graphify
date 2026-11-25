# CLAUDE.md — graphify

## Scopo
`graphifyy` 0.9.50 (PyPI) — skill AI che trasforma cartelle di codice, docs, PDF, immagini e video in un knowledge graph interrogabile. Apache-2.0. Python >= 3.10.

## Struttura
- `graphify/` — pacchetto principale (CLI, detect, extract, build, cluster, analyze, report, export)
- `tests/` — test
- `docs/` — guide (how-it-works, docker-mcp-sqlite, node-summaries-rfc, translations/, superpowers/)
- `worked/` — esempi applicati
- Raiz: README.md, CHANGELOG.md, ARCHITECTURE.md, AGENTS.md, SECURITY.md, BENCHMARKS.md, pyproject.toml, uv.lock, Dockerfile

## Comandi
- Install: `uv tool install graphifyy` (non eseguito in questa tappa — non verificato)
- Verifica test/build: `pytest` — NON eseguito in questa tappa — non verificato
- Comando di verifica del mandato: `m012-verifica.py r4 <worktree> <base> op/M-012-1 graphify` (vedi docs/LLM-GUIDA.md)

## Convenzioni
- Tipi di confidence: EXTRACTED / INFERRED / AMBIGUOUS
- Leiden per le community
- Output: graph.json + GRAPH_REPORT.md + graph.html
- ~31 linguaggi tree-sitter (31 estrattori in graphify/extractors/)

## Non toccare
- Codice in `graphify/` (fuori perimetro di questa tappa)
- `docs/translations/` e `docs/superpowers/` (non revisionati in questa tappa)
- File `docs/_*` (inventario/revisione/lista) — dati di revisione, non riscrivere

## Segreti
Nessuno presente; usare solo segnaposto (es. `API_KEY=`). Non committare valori segreti.

## Rimarcando
Vedi docs/LLM-GUIDA.md per la guida LLM completa (max 120 righe).
