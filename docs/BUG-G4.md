# BUG-G4 — bug graphify (M-031.34b.2)

## BUG-1
Dove: graphify/_minhash.py:48 — `phv = (self._a * hv + self._b) % _MP`
Gravità: alta (hashvalues sbagliati → MinHash/LSH dedup inaffidabile)
Prova: prima della correzione, MinHash(4).update(b'x') → [3985550189 785829723 84915829 791299300]; valori attesi (aritmetica interi Python) → [495309341 2611305435 87106237 1793474420]. `a * hv` overflowa uint64 (a<2^61, hv<2^32 → prodotto<2^93) prima di `% _MP`.
Correzione: calcolo in interi Python (int(a)*hv + int(b)) % mp & 0xFFFFFFFF, array numpy uint64; commit 89e (vedi git log).
Test: tests/test_minhash.py — 11 passed.

## BUG-2
Dove: graphify/_minhash.py:87-95 (`_optimal_lsh_params` / `MinHashLSH.__init__`)
Gravità: non confermato (non è un bug reale)
Prova: riproduzione negativa. Il ciclo `for r in range(1, num_perm // b + 1)` garantisce `r <= num_perm // b` → `b * r <= num_perm` per costruzione; intervalli `hv[i*r:(i+1)*r]` non sono mai vuoti. Numericamente: (128, n=128) → (25,5) b*r=125; (0.7,128) → (14,9) b*r=126; (10,0.5) → (3,3) b*r=9; (7,0.5) → (3,2) b*r=6. Nessuna band vuota. Candidato 2 come enunciato (es. b=64, r=3 → b*r=192>128) è irreproducibile: r=3 non può essere scelto con b=64.
Correzione: nessuna (codice corretto; non si inventa un fix).
Test: tests/test_minhash.py — 11 passed (incl. LSH band structure).
