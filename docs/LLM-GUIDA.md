# LLM-GUIDA — graphify

Guida per un LLM che entra in questo repository. Max 120 righe.

## Cosa è questo repo
- `graphifyy` (PyPI) 0.9.50 — skill/assistente AI per trasformare cartelle di codice, docs, PDF, immagini e video in un knowledge graph interrogabile.
- Licenza Apache-2.0. Python >= 3.10. Build via setuptools (`pyproject.toml`).

## Struttura reale (verificata in esplorazione 2026-11-24)
- `graphify/` — pacchetto principale
- `scripts/`, `tools/` — utilità e tool
- `tests/` — test
- `docs/` — guide: how-it-works.md, docker-mcp-sqlite.md, node-summaries-rfc.md, translations/, superpowers/, _inventario.tsv, _revisione.tsv, _guida-lista.txt
- `worked/` — esempi applicati (README.md in ciascuna sottocartella)
- Raiz: README.md, CHANGELOG.md, ARCHITECTURE.md, AGENTS.md, SECURITY.md, BENCHMARKS.md, Dockerfile, pyproject.toml, uv.lock
- `docs/archivio/` — NON presente al momento (nessun file SUPERATO spostato; R3 non ha spostato nulla).

## Comandi
- `python3 -I ~/openclaw-lab/mandati/verifiche/m012-verifica.py r4 <worktree> 43d54acbfa9e731f7a592bb582c1f4b9d48ed73e op/M-012-1 graphify` — comando di verifica del mandato M-012.1; esito: verranno riportati al commit (vedi Rapporto). Non verificato in anticipo.
- `uv`/`pip install -e .`: non eseguito in questa tappa — non verificato.
- `pytest`: non eseguito in questa tappa — non verificato.

## Note operative
- Niente segreti nei documenti; usati segnaposto.
- Struttura dei docs supervisionata: lista guide in `docs/_guida-lista.txt` (max 12), riveduta in `docs/_revisione.tsv`, allegati nel R1/R2/R3.
- Perimetro di questa tappa: `docs/LLM-GUIDA.md` e `~/graphify-mandati/imparato/graphify.md` — nessun codice, nessun push.
