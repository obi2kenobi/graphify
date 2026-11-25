---
repo: graphifyy
software: [graphify-cli, graphify-mcp, skill-skills, scripts]
aggiornato: 2026-11-25
---

# ISTRUZIONI — uso dei software di questo repo

Breve guida d'uso sintetica per umani e AI. Niente segreti: solo segnaposto `<NOME_VARIABILE>`.

## graphify-cli

### Requisiti
Python >= 3.10, `uv` (consigliato) o `pipx`/`pip`.

### Installazione
`uv tool install graphifyy` (oppure `pipx install graphifyy` / `pip install -e .` per sviluppo).

### Avvio
`graphify install` — copia la skill nell'assistente AI (claude|codex|opencode|aider|amp|agents|claw|droid|trae|gemini|cursor|antigravity|hermes|kiro|pi|devin). `graphify install --project` installa nel progetto.

### Uso
`graphify <comando>` — comandi: `install`, `uninstall`, `path "A" "B"`, `explain "X"`, `diagnose multigraph`, `clone <url>`, `merge-driver`, `merge-graphs`, `add <url>`, `watch`, `serve`. Verifica: `graphify --help` (eseguito: stampa elenco comandi, exit 0).

### Verifica
`graphify --help` → elenco comandi (exit 0).

### Problemi noti
Dipendenze tree-sitter pinnate; assenza di `uv` richiede pip. Niente segreti nel repo.

## graphify-mcp

### Requisiti
Extra `mcp`: `pip install graphifyy[mcp]` (starlette >= 1.3.1).

### Installazione
Come graphify-cli + extra `[mcp]`.

### Avvio
`graphify-mcp` (entry point `graphify.serve:_main`). Avvia il server MCP per esporre il knowledge graph agli assistenti.

### Uso
Configurare l'assistente AI sull'entry point; esporta graph.json/serve. Uso: non verificato in questa sessione.

### Verifica
`graphify-mcp --help` — non verificato.

### Problemi noti
Richiede extra `[mcp]`; HTTP transport usa starlette.

## skill-skills

### Requisiti
Assistente AI supportato (Claude Code, Codex, Cursor, etc.).

### Installazione
`graphify install` copia i file `graphify/skill-*.md` e `graphify/skills/` nella config dell'assistente.

### Avvio
Nelle sessioni dell'assistente: `/graphify`.

### Uso
Mappa cartelle di codice/docs/PDF/immagini/video in knowledge graph interrogabile.

### Verifica
Non verificato in questa sessione (richiede assistente AI attivo).

### Problemi noti
N/A noto.

## scripts / tools

### Requisiti
Come graphify-cli.

### Installazione
`scripts/gen_demo_path.py` è uno script di demo; `tools/skillgen/` genera skill.

### Avvio
`python3 scripts/gen_demo_path.py` — non verificato.

### Uso
Utilità di generazione skill; uso: non verificato.

### Verifica
Non verificato.

### Problemi noti
N/A noto.
