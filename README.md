# malbolge-linguist — Soporte de Malbolge para github-linguist

Workspace **listo en estructura para PR, pero aun no elegible para someterse** a `github-linguist/linguist`. Construido con `EVIDENCE BEFORE NARRATIVE` — sin uso inventado, sin samples de Hello World, sin gramatica no publicada reclamada como lista.

- **Upstream**: `github-linguist/linguist@d5214e1612c858ba14bf98edeca57e1683276f1d` (clone en `upstream/`, gitignored)
- **Branch**: `malbolge-linguist` (este repo, aislado de `C:\Development\ISyCo`)
- **Color**: `#1D1A2F` — morado profundo EVA-01
- **Extension**: `.malbolge` unicamente (`.mal` rechazado, ver abajo)

## Estado — `docs/FINAL_AUDIT.md` (re-audit 2026-09-02)

```
TECHNICAL_IMPLEMENTATION_READY = TRUE
SAMPLE_READY = TRUE
GRAMMAR_READY = TRUE
DETECTION_READY = TRUE
NO_NEW_FAILURES = TRUE
TECHNICAL_WORK = DONE
USAGE_GATE = NOT_DEMONSTRATED
POLICY_ELIGIBLE = FALSE
PR_READY = FALSE
PR_OPEN = FALSE
MAINTAINER_GUIDANCE = RECEIVED
SEMANTIC_ALTERNATIVE_PATH = REJECTED
USAGE_ASSESSMENT = PER_EXTENSION_OR_FILENAME
FINAL_STATE = BLOCKED_BY_USAGE_POLICY
```

La Discussion #8164 recibio guia del maintainer:
https://github.com/github-linguist/linguist/discussions/8164

`@lildude`: "Usage has to be supported per extension or filename being added."

Legacy: `LANGUAGE_DEFINITION_READY=TRUE`, `SAMPLES_READY=TRUE` (estaba BLOCKED, ahora TRUE via sample MIT del PR), `DETECTION_READY` `NOT_DEMONSTRATED`→`TRUE` post-patch, `TESTS_PASS`→`NO_NEW_FAILURES=TRUE` (2/1 vs 2/1), `USAGE_GATE` se queda `NOT_DEMONSTRATED`.

**No abras PR** — la guia del maintainer confirma que `POLICY_ELIGIBLE=FALSE` para la extension `.malbolge` propuesta. El bloqueador es la politica de uso, no la preparacion tecnica.

Epilogo del proyecto historico: [`docs/EPILOGUE.md`](docs/EPILOGUE.md).

## Por que SIGUE BLOQUEADO (politica)

1. **Usage gate** (`CONTRIBUTING.md:236-250`): 2000 archivos (extension comun) / 200 (una vez por repo) el ultimo ano, forks excluidos, distribuido. Medido 2026-09-02 `NOT is:fork`:
   - `extension:malbolge NOT is:fork` = **42** (3 con termino Malbolge)
   - `extension:mal NOT is:fork` = **6096** pero solo 27 Malbolge, fuertemente contaminado (Malabar, Scheme, modelo)
   - Veredicto: `NOT_DEMONSTRATED`. Ninguna busqueda honesta alcanza el umbral. Ver `evidence/github_usage/results_summary.json`. **Ningun repo de DannyBaanks contado**; sin creacion masiva; `CLAIM_SCOPE <= EVIDENCE_SCOPE`.

2. **Gramatica**: `GRAMMAR_PACKAGE_READY=TRUE` (publicado `https://github.com/DannyBaanks/malbolge-syntax` `225f5acb`, MIT, layout `syntaxes/`) y `GRAMMAR_IN_FINAL_UPSTREAM_PATCH=TRUE` (integrado via **canonico** `script/add-grammar https://github.com/DannyBaanks/malbolge-syntax` exit 0 → submodule `vendor/grammars/malbolge-syntax` + `grammars.yml` `source.malbolge` + cache de licencias + `vendor/README.md` via `script/list-grammars`; `test_all_languages_have_grammars` y `test_readme_file_is_in_sync` pasan). Ver `grammar/malbolge-syntax/README.md` y `evidence/patches/malbolge.patch`.

3. **Historia**: PR #4609 (2019, `.mb`, cerrado sin merge, ver `docs/HISTORY_PR4609.md`) se cerro por la misma razon de uso (81k `.mb` pero solo 2 Hello Worlds). La propuesta actual **no repite** `notability=usage`.

## Que esta listo (re-audit)

- **Patch** commit canonico `1af6aef9` (Docker volume `malbolge-canonical-work` `/workspace/patched`, branch `malbolge-canonical`, base `d5214e16`; no pusheado): entrada en `languages.yml` (Mako/Markdown alfabetico, `#1D1A2F`, `.malbolge`, `tm_scope: source.malbolge`, `language_id: 1006177966`), `samples/Malbolge/truth_machine.malbolge` (254 B, SHA `7062713e...`, MIT, mode 100644, ver `docs/SAMPLE_PROVENANCE.md`), patch reproducible `evidence/patches/malbolge.patch` (SHA `DFDA0517F53F95209DEEC4D43A6E287EBDC20C846D14034BFEDFAB57BE4620E8`, `git format-patch d5214e16..1af6aef9`, `git apply` verificado en un clone fresco).

- **Sample** `SAMPLE_READY=TRUE`: `truth_machine.malbolge` — `IN→branch→OUT→HALT/loop` Clasico, `'0'`→halt 136 pasos, `'1'`→loop, cross-verificado `gost`+`oracle`, no es Hello World, procedencia MIT (clausula de sample authored-by-PR, `CONTRIBUTING.md:150-161`).

- **Gramatica** `GRAMMAR_PACKAGE_READY=TRUE` (publicado `https://github.com/DannyBaanks/malbolge-syntax` `225f5acb`, layout `syntaxes/`), `GRAMMAR_IN_FINAL_UPSTREAM_PATCH=TRUE` (integrado via **canonico** `script/add-grammar` exit 0 — submodule, `grammars.yml`, cache de licencias, `vendor/README.md` todos generados por tooling upstream, no escritos a mano). Conservativa (no etiqueta opcodes posicionales erroneamente).

- **Deteccion** `DETECTION_READY=TRUE` post-patch (`evidence/canonical/detection.log`): `FileBlob` → `language=Malbolge`, `extname=.malbolge`, `mime=text/plain`; `Language["Malbolge"]` → `ext:[".malbolge"] color:#1D1A2F id:1006177966 tm_scope:source.malbolge`; end-to-end `github-linguist --breakdown` → `100.00% 254 Malbolge` (`breakdown_cli.log`).

- **Pruebas** `NO_NEW_FAILURES=TRUE` (mismo entorno Docker, `evidence/canonical/`): baseline `rake_test.log` 2034 runs 39353 assertions **2 failures 1 error** vs patched `rake_test_final.log` 2036 runs 39369 assertions **2 failures 1 error** (+2 runs Malbolge sample, +16 assertions, **0 new failures**; los 2 failures+1 error son solo CodeMirror, `vendor/CodeMirror` ausente de un clone fresco, no relacionado con Malbolge).

- Contaminacion: falsos positivos `.mal` (`corkami/mitra` Malabar, `larcenists/larceny` Scheme) — `evidence/github_usage/sample_repositories.md`; sin heuristicas para `.malbolge`.

Pipeline canonico (Docker): volume `malbolge-canonical-work` (`baseline/` fijado `d5214e16`, `patched/` branch `malbolge-canonical`), gem bundle volume `malbolge-canonical-bundle`, DIND `malbolge-canonical-dind`, runner `malbolge-linguist-addgrammar`. Logs crudos completos en `evidence/canonical/`.

## Estructura

```
malbolge-linguist/
  evidence/
    github_usage/          # queries.md, results_summary.json, sample_repositories.md
    canonical/             # logs del pipeline canonico (baseline 2034/2/1, patched 2036/2/1), add_grammar.log, detection.log, breakdown_cli.log, apply_verify.log, environment.log
    tests/                 # logs legacy no-canonicos (preservados por historia)
    patches/malbolge.patch # canonico, d5214e16..1af6aef9, SHA DFDA0517...
  grammar/malbolge-syntax/ # LICENSE MIT, malbolge.tmLanguage.json (source.malbolge), package.json, tests/sample.malbolge + validation.md, README
  PR_DRAFT.md              # replica .github/PULL_REQUEST_TEMPLATE.md, sin check donde esta bloqueado
  TOOLCHAIN_LOCK.json
  README.md                # este archivo
```

El commit canonico del patch `1af6aef9` vive en el Docker volume (`malbolge-canonical-work/patched`, no pusheado); los docs de investigacion nunca entran al patch final. Patch cuando la politica lo permita:

```
lib/linguist/languages.yml  # source.malbolge
samples/Malbolge/truth_machine.malbolge
grammars.yml + vendor/grammars/malbolge-syntax (via script/add-grammar)
vendor/README.md (via script/list-grammars)
vendor/licenses/git_submodule/malbolge-syntax.dep.yml
```

## Para el auditor (GPT)

```powershell
gh repo clone DannyBaanks/malbolge-linguist
cd malbolge-linguist
git log --oneline -5
cat docs/FINAL_AUDIT.md
cat docs/LINGUIST_REQUIREMENTS.md
cat evidence/github_usage/results_summary.json
cat evidence/tests/fileblob.log
cat SHA256SUMS.txt; py -c "import hashlib,pathlib;root=pathlib.Path('.');print(all(hashlib.sha256(p.read_bytes()).hexdigest()==open('SHA256SUMS.txt').read().split()[i*2] for i,p in enumerate(sorted([p for p in root.rglob('*') if p.is_file() and '.git' not in p.parts and p.name!='SHA256SUMS.txt' and 'upstream' not in p.parts]))))"
```

Checar: `upstream/CONTRIBUTING.md:134-250` vs `PR_DRAFT.md`; `evidence/github_usage/queries.md` vs busqueda en GitHub en vivo; `grammar/malbolge-syntax/Malbolge.tmLanguage.json` validez JSON.

## Siguientes pasos (solo queda politica)

1. ~~Publicar `grammar/malbolge-syntax`~~ Listo (`https://github.com/DannyBaanks/malbolge-syntax` `225f5acb`, layout `syntaxes/`, canonico `script/add-grammar` exit 0, patch `evidence/patches/malbolge.patch` `DFDA0517...`)
2. ~~Sample~~ Listo (`SAMPLE_READY=TRUE`, `truth_machine.malbolge` `70627...`)
3. ~~Censo de ProjectMap~~ Listo (demo `evidence/census/corpus` 3 archivos: baseline `verified 1` → con `external.json` `verified 2 rejected 1`; extrapolando GitHub Search `VALID_MALBOLGE` ~71 `UNIQUE_REPOS` ~40-45 < 2000 → `USAGE_GATE=NOT_DEMONSTRATED` final, ver `evidence/census/README.md`)
4. **La Discussion #8164 resolvio la pregunta de politica:** el uso debe soportarse por extension o nombre de archivo propuesto. No se planea accion adicional.

## Links

- Repo: `https://github.com/DannyBaanks/malbolge-linguist`
- Upstream: `https://github.com/github-linguist/linguist`
- Fuente de genealogia (solo lectura): `C:\Development\ISyCo Git\GENEALOGIA_MALBOLGE`

*EVIDENCE BEFORE NARRATIVE. Sin uso inventado. EVA-01 #1D1A2F.*
