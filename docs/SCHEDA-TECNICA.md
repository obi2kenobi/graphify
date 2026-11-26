---
repo: graphifyy
linguaggi: Python >= 3.10
stato: attivo
aggiornato: 2026-11-26
---

# Scheda tecnica — graphify

## Scopo
`graphifyy` 0.9.50 (PyPI, Apache-2.0): skill/assistente AI che trasforma cartelle di codice, docs, PDF, immagini e video in un knowledge graph interrogabile. Pubblicato su PyPI e distribuito come skill per assistenti AI (Claude Code, Codex, Cursor, OpenCode, Aider, Gemini CLI, etc.).

## Architettura
Pipeline: detect → extract → build → cluster → analyze → report → export. Pacchetto principale `graphify/` (CLI, detect, extract, build, cluster, analyze, report, export, mcp, serve, wiki). Tree-sitter per ~31 linguaggi (`graphify/extractors/`). Confidence tags: EXTRACTED / INFERRED / AMBIGUOUS. Clustering Leiden. Output: graph.json + GRAPH_REPORT.md + graph.html.

## Componenti
| Nome | Ruolo | File |
|---|---|---|
| CLI | entry point `graphify` | graphify/cli.py, graphify/__main__.py |
| detect | rilevamento file/tipi | graphify/detect.py |
| extract | estrazione (tree-sitter, LLM) | graphify/extract.py, graphify/extractors/ |
| build | costruzione grafo | graphify/build.py |
| cluster | community detection (Leiden) | graphify/cluster.py |
| analyze | analisi/statistiche | graphify/analyze.py |
| report | GRAPH_REPORT.md | graphify/report.py |
| export | exporter graph.json/html | graphify/export.py, graphify/exporters/ |
| mcp/serve | server MCP HTTP | graphify/serve.py, graphify/mcp_ingest.py |
| skill | skill copia assistenti AI | graphify/skill.md, graphify/skill-*.md, graphify/skills/ |

## Dati e interfacce
- Input: cartelle di codice/docs/PDF/immagini/video.
- Output: graph.json, GRAPH_REPORT.md, graph.html; integrazione MCP (`graphify-mcp`, entry point `graphify.serve:_main`); graphify-cli comandi: install, uninstall, path, explain, diagnose, clone, merge-driver, merge-graphs, add, watch, serve.
- Connessione assistenti AI via skill installata in config dell'assistente (`graphify install`).

## Dipendenze
- Runtime: networkx, numpy, rapidfuzz, tree-sitter (+~28 grammar tree-sitter), Python >= 3.10.
- Extra: `mcp` (mcp>=1,<3, starlette>=1.3.1,<2), `neo4j`, `falkordb`, `pdf` (pypdf, markdownify), `watch` (watchdog), `svg` (matplotlib), `leiden` (graspologic, <3.13), `office` (python-docx, openpyxl), `google` (openpyxl), postgres (tree-sitter-sql).
- Build: setuptools>=77.

## Configurazione
Variabili d'ambiente (solo nomi, nessun valore): `ANTHROPIC_API_KEY`, `ANTHROPIC_BASE_URL`, `ANTHROPIC_MODEL`, `GEMINI_API_KEY` / `GOOGLE_API_KEY`, `OPENAI_API_KEY`, `OPENAI_BASE_URL`, `OPENAI_MODEL`, `DEEPSEEK_API_KEY`, `MOONSHOT_API_KEY`, `OLLAMA_BASE_URL`, `OLLAMA_MODEL`, `GRAPHIFY_OLLAMA_NUM_CTX`, `GRAPHIFY_OLLAMA_KEEP_ALIVE`, `AZURE_OPENAI_API_KEY`, `AZURE_OPENAI_ENDPOINT`, `AZURE_OPENAI_API_VERSION`. Segreti mai committati.

## Build e test
- Build: `pyproject.toml` (setuptools), uv.lock presente. `uv tool install graphifyy` — non eseguito — non verificato.
- Test: `pytest` — non eseguito in questa tappa — non verificato.

## Deploy
Pubblicazione PyPI come `graphifyy`. No CI/CD verificato in questa tappa. Dockerfile presente (non verificato).

## Rischi e debito tecnico
- Dipendenze tree-sitter pinnate; versioni stringenti limitano compatibilità.
- Extra espandono superficie (mcp, leiden, neo4j, postgres); versioni pinnate conservatrici.
- Alcuni comandi verificati solo parzialmente (`graphify --help` exit 0); `pytest` e installazione non verificati.
- Nessun segreto nel repo; uso segnaposto solo.
