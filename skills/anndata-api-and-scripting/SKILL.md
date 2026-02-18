---
name: anndata-api-and-scripting
description: This skill should be used when users ask about api and scripting in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: API and Scripting

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (small real IO run):
```bash
python - <<'PY'
import numpy as np
import pandas as pd
import anndata as ad

adata = ad.AnnData(X=np.arange(12).reshape(3, 4), obs=pd.DataFrame(index=["c1", "c2", "c3"]))
adata.write_h5ad("/tmp/api_bootstrap.h5ad")
roundtrip = ad.read_h5ad("/tmp/api_bootstrap.h5ad")
print(roundtrip.shape)
PY
```
Validation checkpoint: printed shape must be `(3, 4)` before deeper API debugging.

## High-Signal Playbook

### Route conditions
- Route to `anndata-parallel-hpc` for zarr-v3 performance, sharding, consolidated metadata, or remote-store lazy reads (`docs/tutorials/zarr-v3.md`).
- Route to `anndata-release-notes` for upgrade deltas or behavior changes across versions (`docs/release-notes/index.md`).
- Route to `anndata-typing` for type-alias semantics and annotation boundaries (`docs/typing.md`).
- Route to `anndata-advanced-topics` for concatenation, fileformat prose, interoperability, and references.

### Triage questions
- Are you reading/writing full `AnnData` objects or individual elements?
- Is the target format `.h5ad`, `zarr`, or a non-native import/export path?
- Do you need only stable API calls, or are experimental APIs acceptable?
- Are you implementing accessor-based references (`anndata.acc`) or direct object access?
- Do you need custom namespace extension via `register_anndata_namespace`?
- Is the store local, remote, and/or consolidated?

### Canonical workflow
1. Start in `docs/api.md` to pick public API surface.
2. Use stable IO first: `read_h5ad`, `read_zarr`, `AnnData.write_h5ad`, `AnnData.write_zarr` (`docs/api.md`).
3. Use element-level IO for partial updates/reads: `io.read_elem` / `io.write_elem` (`docs/api.md`).
4. Use `anndata.acc` references for object-independent selectors (`docs/accessors.rst`).
5. Use experimental APIs only if stable APIs are insufficient (`docs/api.md`, experimental warning).
6. For extension namespaces, follow `register_anndata_namespace` requirements (`docs/api.md`, `src/anndata/_core/extensions.py`).
7. If unresolved, inspect `references/source_map.md` from top to bottom.

### Minimal working example
```python
import anndata as ad
import zarr

adata = ad.read_h5ad("input.h5ad")
adata.write_zarr("out.zarr")

g = zarr.open_group("out.zarr", mode="r")
obs = ad.io.read_elem(g["obs"])
```

```python
from anndata.acc import A

ref = A.obsm["pca"][:, 0]
if ref in adata:
    first_pc = adata[ref]
```

### Pitfalls and fixes
- Experimental APIs are explicitly unstable; pin versions and prefer stable APIs first (`docs/api.md`).
- Non-native formats may not preserve full AnnData structure; rebuild from parts when needed (`docs/api.md`, Reading tip).
- `anndata.acc` objects are references, not loaded arrays; dereference against a concrete `adata` (`docs/accessors.rst`).
- Namespace registration requires `__init__(self, adata: AnnData)`; otherwise runtime checks fail (`src/anndata/_core/extensions.py`).
- Lazy-chunk behavior changed in 0.12.1; validate chunk assumptions during upgrades (`docs/release-notes/0.12.1.md`).
- Mutating consolidated zarr stores requires unconsolidated write + reconsolidation (`docs/tutorials/zarr-v3.md`).

### Convergence/validation checks
- Round-trip a fixture through the chosen IO path and compare `n_obs`, `n_vars`, and key containers.
- Verify element-level IO writes produce expected key paths and encoding metadata.
- Check `ref in adata` before using accessor-generated references.
- Validate custom namespace registration and accessor caching on first access.

## Scope
- Handle questions about language bindings, APIs, and programmatic interfaces.
- Keep responses architectural unless the request explicitly asks for symbol-level behavior.

## Primary documentation references
- `docs/api.md`
- `docs/accessors.rst`
- `docs/_templates/autosummary/class.rst`
- `docs/_templates/autosummary/class-minimal.rst`

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
- `src/anndata/_io/h5ad.py` (`read_h5ad`, `write_h5ad`, `read_h5ad_backed`)
- `src/anndata/_io/zarr.py` (`read_zarr`, `write_zarr`, `is_group_consolidated`)
- `src/anndata/_io/specs/registry.py` (`read_elem`, `read_elem_lazy`, `write_elem`, `read_elem_partial`)
- `src/anndata/_core/extensions.py` (`register_anndata_namespace`, `_check_namespace_signature`)
- `src/anndata/_core/anndata.py` (`AnnData.__getitem__`, `AnnData.write_h5ad`, `AnnData.write_zarr`)
- `src/anndata/acc/__init__.py` (`AdRef`, `AdAcc`, `MapAcc`)
- `src/anndata/experimental/_dispatch_io.py` (`read_dispatched`, `write_dispatched`)
- `src/anndata/experimental/multi_files/_anncollection.py` (`AnnCollection`, `AnnCollectionView`)
- `src/anndata/experimental/pytorch/_annloader.py` (`AnnLoader`, `default_converter`)
- `src/anndata/io.py` (public re-exports for `read_h5ad`, `read_zarr`, `read_elem`, `write_elem`)
- `src/anndata/__init__.py` (top-level exports and compatibility warnings)
- Prefer targeted source search (for example: `rg -n "<symbol_or_keyword>" src/anndata tests`).
