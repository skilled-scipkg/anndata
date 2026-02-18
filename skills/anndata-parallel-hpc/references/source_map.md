# anndata source map: Parallel and HPC

Generated from source roots:
- `src/anndata`
- `src/testing/anndata`

Use this map only after exhausting the topic docs in `references/doc_map.md`.

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

## Topic query tokens
- `zarr_write_format`
- `auto_shard_zarr_v3`
- `consolidate_metadata`
- `read_lazy`
- `read_elem_lazy`
- `chunks`
- `shards`
- `write_dispatched`
- `read_dispatched`

## Fast source navigation
- `rg -n "zarr_write_format|auto_shard_zarr_v3|validate_zarr" src/anndata/_settings.py`
- `rg -n "consolid|zarr_format|chunks|shard|open_write_group" src/anndata/_io/zarr.py src/anndata/_io/specs`
- `rg -n "read_lazy|read_elem_lazy|resolve_chunks" src/anndata/experimental src/anndata/_io/specs/lazy_methods.py`

## Suggested source entry points (function-level)
- `src/anndata/_io/zarr.py` | `write_zarr`, `read_zarr`, `open_write_group`, `is_group_consolidated`
- `src/anndata/experimental/backed/_io.py` | `read_lazy`
- `src/anndata/_io/specs/registry.py` | `read_elem_lazy`, `read_elem_partial`
- `src/anndata/_io/specs/lazy_methods.py` | `resolve_chunks`, `read_sparse_as_dask`, `read_zarr_array`
- `src/anndata/experimental/_dispatch_io.py` | `read_dispatched`, `write_dispatched`
- `src/anndata/_settings.py` | `validate_zarr_write_format`, `validate_zarr_sharding`
- `src/anndata/_io/utils.py` | `report_read_key_on_error`, `report_write_key_on_error`
- `tests/lazy/test_read.py` | `test_unconsolidated`, `test_chunks_df`, `test_access_count_elem_access`
- `tests/test_readwrite.py` | `test_readwrite_equivalent_h5ad_zarr`, `test_zarr_compression`

## Function probes
```bash
rg -n "def (write_zarr|read_zarr|open_write_group|is_group_consolidated)\\(" src/anndata/_io/zarr.py
rg -n "def read_lazy\\(" src/anndata/experimental/backed/_io.py
rg -n "def (read_elem_lazy|read_elem_partial)\\(" src/anndata/_io/specs/registry.py
rg -n "def (resolve_chunks|read_sparse_as_dask|read_zarr_array)\\(" src/anndata/_io/specs/lazy_methods.py
rg -n "def (validate_zarr_write_format|validate_zarr_sharding)\\(" src/anndata/_settings.py
rg -n "def (test_unconsolidated|test_chunks_df|test_zarr_compression)\\(" tests/lazy/test_read.py tests/test_readwrite.py
```

## Validation checkpoint
- Probes must find all named functions/tests and no referenced file should be missing before performance tuning or simulation scaling work.
