---
name: anndata-parallel-hpc
description: This skill should be used when users ask about parallel and hpc in anndata; it prioritizes documentation references and then source inspection only for unresolved details.
---

# anndata: Parallel and HPC

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

Simulation bootstrap (lazy/zarr behavior):
```bash
python - <<'PY'
import anndata as ad
import numpy as np

adata = ad.AnnData(X=np.eye(6))
adata.write_zarr("/tmp/hpc_bootstrap.zarr")
lazy = ad.experimental.read_lazy("/tmp/hpc_bootstrap.zarr")
print(lazy.shape)
PY
```
Validation checkpoint: shape output must be `(6, 6)` and no consolidation/read errors should occur.

## High-Signal Playbook

### Route conditions
- Route to `anndata-api-and-scripting` for general API usage not dominated by zarr-v3/runtime scaling details.
- Route to `anndata-troubleshooting` when failures are compatibility or warning-driven rather than performance/layout tuning.
- Route to `anndata-release-notes` when issue appears version-specific (for example 0.12.1 lazy chunking fixes).

### Triage questions
- Is the workload local filesystem, network filesystem, or remote object storage?
- Are you mutating an existing consolidated zarr store?
- Are you using `read_lazy`/`read_elem_lazy`, and what chunk strategy is expected?
- Is zarr format v2 or v3 required?
- Do you need sharding or custom codec pipelines?
- Are GPU IO or async APIs mandatory requirements?

### Canonical workflow
1. Start with `docs/tutorials/zarr-v3.md` for current defaults and constraints.
2. Confirm write format settings (`anndata.settings.zarr_write_format`) and consolidation assumptions.
3. For in-place mutations, open unconsolidated, write, then reconsolidate metadata.
4. For remote reads, prefer consolidated stores and `experimental.read_lazy`.
5. Tune chunks/shards only after baseline correctness is proven.
6. Escalate to Rust zarr codec pipeline only when measured throughput needs justify it.
7. For unresolved behavior, inspect `_io/zarr.py`, `experimental/backed/_io.py`, and specs registry.

### Minimal working example
```python
import anndata as ad
import pandas as pd
import zarr

g = zarr.open_group("data.zarr", mode="a", use_consolidated=False)
obs = pd.DataFrame({"batch": [0, 1]}, index=["c0", "c1"])
ad.io.write_elem(g, "obs", obs, dataset_kwargs={"chunks": (250,)})
zarr.consolidate_metadata(g.store)
```

```python
import anndata as ad
import zarr

g = zarr.open("data.zarr", mode="r")
lazy_x = ad.experimental.read_elem_lazy(g["X"], chunks=(500, -1))
```

### Pitfalls and fixes
- Mutating a consolidated store directly can fail; use unconsolidated mode and reconsolidate afterward (`docs/tutorials/zarr-v3.md`).
- Stale consolidated metadata causes inconsistent reads after structural edits; always reconsolidate (`docs/tutorials/zarr-v3.md`).
- Sharding is effectively a zarr-v3 path; for custom sharding use dispatched writes (`docs/tutorials/zarr-v3.md`).
- Remote lazy reads without consolidated metadata can be incomplete or very slow (`docs/tutorials/zarr-v3.md`).
- GPU IO is not broadly supported yet; dense-only paths may work but are untested (`docs/tutorials/zarr-v3.md`).
- anndata currently exports no async IO API; avoid planning around async public calls (`docs/tutorials/zarr-v3.md`).

### Convergence/validation checks
- Validate the store is consolidated after writes.
- Confirm lazy chunk sizes match intent (especially sparse minor axis constraints).
- Compare small read/write benchmarks before and after sharding/codec changes.
- Verify round-tripped `AnnData` shape and key containers after tuning.

## Scope
- Handle questions about MPI/OpenMP/GPU execution, scaling, and batch systems.
- Keep responses abstract and architectural for large codebases; avoid exhaustive per-function documentation unless requested.

## Primary documentation references
- `docs/tutorials/zarr-v3.md`
- `docs/contributing.md`
- `docs/release-notes/0.12.1.md`
- `docs/release-notes/0.11.2.md`

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
- `src/anndata/_io/zarr.py` (`write_zarr`, `read_zarr`, `open_write_group`, `is_group_consolidated`)
- `src/anndata/experimental/backed/_io.py` (`read_lazy`)
- `src/anndata/_io/specs/registry.py` (`read_elem_lazy`, `read_elem_partial`)
- `src/anndata/_io/specs/lazy_methods.py` (`resolve_chunks`, `read_sparse_as_dask`, `read_zarr_array`)
- `src/anndata/experimental/_dispatch_io.py` (`read_dispatched`, `write_dispatched`)
- `src/anndata/_settings.py` (`validate_zarr_write_format`, `validate_zarr_sharding`)
- `src/anndata/_io/utils.py` (`report_read_key_on_error`, `report_write_key_on_error`)
- `tests/lazy/test_read.py` (`test_unconsolidated`, `test_chunks_df`, `test_access_count_elem_access`)
- `tests/test_readwrite.py` (`test_readwrite_equivalent_h5ad_zarr`, `test_zarr_compression`)
- Prefer targeted source search (for example: `rg -n "zarr|read_lazy|read_elem_lazy|shard|consolid" src/anndata tests`).
