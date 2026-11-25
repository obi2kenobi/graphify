# LLM-GUIDA — graphify

Guida per un LLM che entra in questo repository. Max 120 righe.

## Cosa è questo repo
- `graphifyy` (PyPI) 0.9.50 — skill/assistente AI per trasformare cartelle di codice, docs, PDF, immagini, video in un knowledge graph interrogabile.
- Apache-2.0. Python >= 3.10. Build setuptools (`pyproject.toml`).

## Struttura reale (verificata 2026-11-24/25)
- `graphify/` — pacchetto principale (detect, extract, build, cluster, analyze, report, export)
- `scripts/`, `tools/` — utilità
- `tests/` — test
- `docs/` — how-it-works.md, docker-mcp-sqlite.md, node-summaries-rfc.md, translations/ (~32), superpowers/ (plan+spec), _inventario.tsv, _revisione.tsv, _guida-lista.txt
- `worked/` — esempi applicati
- Raiz: README.md, CHANGELOG.md (1901 righe), ARCHITECTURE.md, AGENTS.md, SECURITY.md, BENCHMARKS.md, Dockerfile, pyproject.toml, uv.lock
- `docs/archivio/` — NON presente (nessun file spostato; R3 non ha spostato nulla)

## Comandi
- Verifica del mandato: `python3 -I ~/openclaw-lab/mandati/verifiche/m012-verifica.py r4 <worktree> 43d54acbfa9e731f7a592bb582c1f4b9d48ed73e op/M-012-1 graphify` — non verificato in anticipo in questa tappa.
- `uv tool install graphifyy` / `pip install -e .` — NON eseguito — non verificato.
- `pytest` — NON eseguito — non verificato.

## Confidence e pipeline
- Pipeline: detect → extract → build → cluster → analyze → report → export.
- Tags di confidence: EXTRACTED / INFERRED / AMBIGUOUS.
- Leiden per le community.
- Output: graph.json, GRAPH_REPORT.md, graph.html.

## Struttura dei docs supervisionata
- Lista guide (max 12): `docs/_guida-lista.txt`
- Revisione (classi esatte): `docs/_revisione.tsv` (6 colonne: file, classe, affermazione, atteso, trovato, esito)
- Inventario: `docs/_inventario.tsv` (documento, righe, ultimo_commit)

## Note operative
- Nessuno segreto nei documenti; solo segnaposto.
- 31 extractor tree-sitter in graphify/extractors/ (non ~40).
- Perimetro tappa M-017.152: CLAUDE.md, docs/LLM-GUIDA.md, imparato/graphify.md, docs/_*. Nessun codice, nessun push.
