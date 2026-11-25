# BUG-G4 — candidati bug graphify (M-031.34b.1)

Analisi statica + riproduzione aritmetica (numpy non disponibile nel sistema base;
simulazioni pure-Python). Nessuna correzione applicata.

## Candidati

CANDIDATO-1:** graphify/_minhash.py:48 — `phv = (self._a * hv + self._b) % _MP`  — `a * hv` in uint64 overflowa (a < 2^61, hv < 2^32 → prodotto < 2^93) prima di `% _MP`, contraddicendo il docstring "Hash family equivalent to datasketch". Risultato: hashvalues sbagliati → MinHash/LSH del dedup inaffidabile.

CANDIDATO-2:** graphify/_minhash.py:87-95 (`_optimal_lsh_params` / `MinHashLSH.__init__`) — `r` può portare `b * r > num_perm` (es. b=64, r=3 → b*r=192 > 128); la slicing `hv[i*r:(i+1)*r]` diventa vuota per le bande finali (numpy clamp) → `tobytes()` = `b''` → ogni coppia di chiavi collide nella band vuota → falso match schiaccianti nel dedup.

## Note

- Candidato 1: riproduzione pura-Python (simulazione uint64): correct=129723069474764036 vs actual=1274943748 (con a=1234567890123456789 % (2^61-1), hv=0xDEADBEEF). Non matching.
- Candidato 2: b*r > num_perm dimostrabile per i valori di b non-ottimo; il parametro scelto per threshold=0.7/num_perm=128 è (14, 9) → b*r=126 ≤ 128, non raggiunto in questo caso, ma l'invariante non è garantito dal codice.
