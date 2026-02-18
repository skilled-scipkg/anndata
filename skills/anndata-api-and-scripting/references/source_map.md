# anndata source map: API and Scripting

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
- `read_h5ad`
- `read_zarr`
- `write_h5ad`
- `write_zarr`
- `read_elem`
- `write_elem`
- `read_elem_lazy`
- `register_anndata_namespace`
- `AdRef`
- `AnnCollection`
- `AnnLoader`

## Fast source navigation
- `rg -n "read_h5ad|read_zarr|write_h5ad|write_zarr|read_elem|write_elem" src/anndata`
- `rg -n "register_anndata_namespace|AdRef|AdAcc|AnnCollection|AnnLoader" src/anndata`
- `rg -n "read_dispatched|write_dispatched|read_elem_lazy" src/anndata/experimental src/anndata/_io/specs`

## Suggested source entry points (function-level)
- `src/anndata/_io/h5ad.py` | `read_h5ad`, `read_h5ad_backed`, `write_h5ad`
- `src/anndata/_io/zarr.py` | `read_zarr`, `write_zarr`, `is_group_consolidated`
- `src/anndata/_io/specs/registry.py` | `read_elem`, `read_elem_lazy`, `write_elem`, `read_elem_partial`
- `src/anndata/_core/extensions.py` | `register_anndata_namespace`, `_check_namespace_signature`
- `src/anndata/_core/anndata.py` | `AnnData.write_h5ad`, `AnnData.write_zarr`, `AnnData.__getitem__`
- `src/anndata/acc/__init__.py` | `AdRef`, `AdAcc`, `MapAcc`
- `src/anndata/experimental/_dispatch_io.py` | `read_dispatched`, `write_dispatched`
- `src/anndata/experimental/multi_files/_anncollection.py` | `AnnCollection`, `AnnCollectionView`
- `src/anndata/experimental/pytorch/_annloader.py` | `AnnLoader`, `default_converter`
- `src/anndata/io.py` | public re-exports for `read_h5ad`, `read_zarr`, `read_elem`, `write_elem`

## Function probes
```bash
rg -n "def (read_h5ad|read_h5ad_backed|write_h5ad)\\(" src/anndata/_io/h5ad.py
rg -n "def (read_zarr|write_zarr|is_group_consolidated)\\(" src/anndata/_io/zarr.py
rg -n "def (read_elem|read_elem_lazy|write_elem|read_elem_partial)\\(" src/anndata/_io/specs/registry.py
rg -n "def (register_anndata_namespace|_check_namespace_signature)\\(" src/anndata/_core/extensions.py
rg -n "def (read_dispatched|write_dispatched)\\(" src/anndata/experimental/_dispatch_io.py
rg -n "class (AdRef|AdAcc|AnnCollection|AnnLoader)" src/anndata/acc/__init__.py src/anndata/experimental/multi_files/_anncollection.py src/anndata/experimental/pytorch/_annloader.py
```

## Validation checkpoint
- Every probe above should return at least one hit before doing deeper implementation/debugging work.
