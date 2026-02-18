---
name: anndata-typing
description: This skill should be used when users ask about typing in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: Typing

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (typing + runtime boundary check):
```bash
python - <<'PY'
import anndata as ad
import numpy as np
from anndata.typing import Index1D

adata = ad.AnnData(np.eye(4))
obs_idx: Index1D = [0, 2]
print(adata[obs_idx, :].shape)
PY
```
Validation checkpoint: indexing result should have shape `(2, 4)` and use public aliases only.

## High-Signal Playbook

### Route conditions
- Route to `anndata-api-and-scripting` for API behavior questions beyond annotation semantics.
- Route to `anndata-troubleshooting` when failures are runtime IO/compat issues, not type design.
- Route to `anndata-release-notes` if a type-related behavior changed across versions.

### Triage questions
- Is the question about static analysis, runtime behavior, or both?
- Is the target alias `Index1D`, `Index`, `AxisStorable`, or `RWAble`?
- Is this for user-facing annotations or internal protocol/dispatch code?
- Are private internal types (`anndata._types`) being used accidentally?
- Is the code path tied to IO dispatch (`read_elem` / `write_elem`)?

### Canonical workflow
1. Start with `docs/typing.md` for exported typing surface.
2. Resolve alias definitions in `src/anndata/typing.py`.
3. Distinguish public aliases (`anndata.typing`) from internal protocols (`src/anndata/_types.py`).
4. If IO typing behavior is involved, map to specs registry dispatch.
5. Validate assumptions with static checking plus focused runtime tests.

### Minimal working example
```python
import anndata as ad
from anndata.typing import Index1D, RWAble


def subset_obs(adata: ad.AnnData, obs_index: Index1D):
    return adata[obs_index, :]


payload: RWAble = {"flag": [True, False, True]}
```

### Pitfalls and fixes
- `type` aliases are not runtime classes; do not use `isinstance(..., Index1D)` (`src/anndata/typing.py`).
- `RWAble` is broader than `AxisStorable` and includes `AnnData`/extension arrays (`src/anndata/typing.py`).
- Internal `_types.py` protocols are implementation details; prefer public aliases for user code (`src/anndata/_types.py`).
- `Index` includes ellipsis/tuple forms; shape assumptions should be explicit in API contracts (`src/anndata/typing.py`).
- `docs/typing.md` is intentionally minimal; source inspection is required for nuance (`docs/typing.md`).

### Convergence/validation checks
- Confirm static checker acceptance for intended annotation surface.
- Verify representative `Index1D` variants (slice, boolean mask, name list) on real `AnnData` objects.
- Validate `RWAble` payloads through `io.write_elem`/`io.read_elem` where relevant.
- Ensure no private type aliases leak into public signatures.

## Scope
- Handle questions about documentation grouped under the 'typing' theme.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/typing.md`

## Workflow
- Start with the primary references above.
- If details are missing, inspect `references/doc_map.md` for the complete topic document list.
- Use tutorials/examples as executable usage patterns when available.
- Use tests as behavior or regression references when available.
- If ambiguity remains after docs, inspect `references/source_map.md` and start with the ranked source entry points.
- Cite exact documentation file paths in responses.

## Tutorials and examples
- `docs/tutorials`

## Test references
- `tests`
- `src/anndata/tests`

## Optional deeper inspection
- `src/anndata`
- `src/testing/anndata`

## Source entry points for unresolved issues
- `src/anndata/typing.py` (type aliases `Index1D`, `Index`, `AxisStorable`, `RWAble`)
- `src/anndata/_types.py` (protocols `_ReadInternal`, `Read`, `ReadLazy`, `Write`, `ReadCallback`, `WriteCallback`)
- `src/anndata/types.py` (public protocols `ExtensionNamespace`, `SupportsArrayApi`)
- `src/anndata/_core/anndata.py` (`AnnData.__getitem__` runtime boundary for index aliases)
- `src/anndata/_io/specs/registry.py` (`read_elem`, `read_elem_lazy`, `write_elem` typing boundary)
- `src/anndata/io.py` (public IO exports used in typed user code)
- Prefer targeted source search (for example: `rg -n "type Index|AxisStorable|RWAble|Protocol" src/anndata`).
