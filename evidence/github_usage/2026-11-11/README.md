# Medición de uso + PR #8329 — 2026-11-11

Evidencia cruda: `raw_search.txt` (salida de `gh api search/code`), `pr_8329.json` (`gh pr view`), `pr_8329_body.md` (cuerpo enviado).

| Query (REST code search) | 2026-09-02 | 2026-11-11 |
|---|---|---|
| `extension:malbolge NOT is:fork` | 42 | **37** |
| `extension:mal malbolge` | 27 | 26 |
| `extension:mb malbolge` | — | 12 |
| `malbolge` (cualquier mención) | — | 9424 |

- El buscador web mostró ~12k para `malbolge` (captura de Danny). Web y REST son índices distintos: no se suman ni se comparan.
- Las menciones son evidencia de **ecosistema**, no de **uso por extensión**. El umbral (`CONTRIBUTING.md:245`) sigue siendo 2000 archivos `.malbolge`.
- `USAGE_GATE = NOT_DEMONSTRATED` (sin cambio).

## PR

- https://github.com/github-linguist/linguist/pull/8329, abierto 2026-11-11T20:21:50Z por decisión de Danny, como **solicitud explícita de excepción**. El PR no afirma que se cumpla la política.
- Head `248e9972` en `DannyBaanks/linguist:add-malbolge`: patch canónico `evidence/patches/malbolge.patch` (SHA `DFDA0517…`), aplicado sin conflictos con `git am --3way` sobre el `main` de upstream `d456527f`. El autor se cambió a la noreply de GitHub; el contenido no cambió.
- `NOT_DEMONSTRATED`: la suite de pruebas no se volvió a correr sobre `d456527f`. La evidencia de 0 fallas nuevas es de la base `d5214e16`. Para la nueva base cuenta el CI del PR.
