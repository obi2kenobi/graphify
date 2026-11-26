# BUG-G5 — Caccia ai bug gravi (M-032.34b)

NON TROVATO: nessun bug grave nuovo confermato entro il tempo disponibile (15 min), diverso da BUG-G4.md.

## Esclusione (BUG-G4, da non ripetere)
- BUG-1 G4: overflow uint64 in `graphify/_minhash.py:48` (corretto su fix/g4-2026-11).
- BUG-2 G4: candidato `_optimal_lsh_params` in `graphify/_minhash.py:87-95`, dichiarato non-bug.

## File letti (integralmente o quasi)
- `graphify/validate.py` (95 righe): gestione id non-hashable corretta, nessun crash.
- `graphify/cluster.py` (320 righe): `cohesion` protetto a riga 265 (`if possible > 0 else 0.0`).
- `graphify/affected.py` (318 righe): normalizzazione edges→links corretta (#738, #1174, #1198).
- `graphify/global_graph.py` (184 righe): manifest corrotto → backup `.corrupt.<ts>`, non cancellazione.
- `graphify/report.py` (325 righe): divisioni protette (r.120 `total = len(...) or 1`; r.126 guardia `if inf_scores`).
- `graphify/benchmark.py` (r.95-132): divisione a r.122 protetta da `if not per_question: return` a r.117. NON-bug.
- `graphify/extract.py` (r.5575-5660): divisioni a r.5586 e r.5642 irraggiungibili con lista vuota (loop non incrementa i contatori). NON-bug.

## Ricerche fatte (grep su graphify/*.py)
- Default mutabili / `is "..."` / `== True`: solo falsi positivi in commenti.
- `TODO|FIXME|XXX|HACK|BUG`: solo riferimenti storici (#BUG1, #BUG2, #738, #1174, #1198).
- Divisioni `/` e `//`: tutti i candidati verificati risultano protetti (vedi sopra).
- `.pop(` / `del` / `.remove(` durante iterazioni: nessuna mutazione-durante-iterazione confermata.
- `except Exception` in cache.py:34,389,1097; dedup.py:360,547,978; extract.py (15 punti); build.py:455: non verificati uno a uno per tempo.

## Non verificato (manca per tempo)
- File grandi non letti per intero: `extract.py` (7162 righe), `serve.py` (2387), `build.py` (2070), `watch.py` (2059), `export.py` (1349), `cache.py` (1706), `dedup.py` (979), `analyze.py` (749).
- Gli `except Exception` mappati potrebbero nascondere perdita dati silenziosa: non verificato.
- Test del repo non eseguiti (nessuna modifica al codice fatta).
