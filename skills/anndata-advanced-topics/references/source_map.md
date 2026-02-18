# anndata source map: Advanced Topics

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
- `concat`
- `merge`
- `encoding_type`
- `encoding_version`
- `h5ad`
- `zarr`
- `interoperability`
- `references`
- `benchmarks`

## Fast source navigation
- `rg -n "def concat|def merge_nested|def check_combinable_cols" src/anndata/_core/merge.py`
- `rg -n "def concat_on_disk|def _concat_on_disk_inner" src/anndata/experimental/merge.py`
- `rg -n "def (read_elem|read_elem_lazy|write_elem)\\(|class IOSpec" src/anndata/_io/specs/registry.py`
- `rg -n "def (read_h5ad|write_h5ad|read_zarr|write_zarr)\\(" src/anndata/_io/h5ad.py src/anndata/_io/zarr.py`

## Suggested source entry points (function-level)
- `src/anndata/_core/merge.py` | `concat`, `merge_nested`, `check_combinable_cols`
- `src/anndata/experimental/merge.py` | `concat_on_disk`, `_concat_on_disk_inner`
- `src/anndata/_io/specs/registry.py` | `IOSpec`, `read_elem`, `read_elem_lazy`, `write_elem`
- `src/anndata/_io/specs/methods.py` | `write_anndata`, `read_anndata`, `read_partial`
- `src/anndata/_io/h5ad.py` | `read_h5ad`, `write_h5ad`
- `src/anndata/_io/zarr.py` | `read_zarr`, `write_zarr`
- `src/anndata/compat/__init__.py` | `_read_attr`, `_from_fixed_length_strings`, `_decode_structured_array`
- `src/anndata/_core/anndata.py` | `AnnData.concatenate`, `AnnData.write_h5ad`, `AnnData.write_zarr`
- `benchmarks/benchmarks/readwrite.py` | `H5ADReadSuite`, `H5ADWriteSuite`, `H5ADBackedWriteSuite`

## Function probes
```bash
rg -n "def (concat|merge_nested|check_combinable_cols)\\(" src/anndata/_core/merge.py
rg -n "def (concat_on_disk|_concat_on_disk_inner)\\(" src/anndata/experimental/merge.py
rg -n "def (read_elem|read_elem_lazy|write_elem)\\(|class IOSpec" src/anndata/_io/specs/registry.py
rg -n "def (write_anndata|read_anndata|read_partial)\\(" src/anndata/_io/specs/methods.py
rg -n "def (read_h5ad|write_h5ad|read_zarr|write_zarr)\\(" src/anndata/_io/h5ad.py src/anndata/_io/zarr.py
rg -n "class (H5ADReadSuite|H5ADWriteSuite|H5ADBackedWriteSuite)" benchmarks/benchmarks/readwrite.py
```

## Validation checkpoint
- At least one probe hit per listed file is required before using that file as evidence in an answer.
