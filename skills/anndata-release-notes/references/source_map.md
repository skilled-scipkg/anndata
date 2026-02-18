# anndata source map: Release Notes

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
- `copy_on_write_X`
- `read_elem_lazy`
- `OldFormatWarning`
- `backwards compat`
- `FutureWarning`
- `read_h5ad`
- `read_zarr`

## Fast source navigation
- `rg -n "__version__|OldFormatWarning|__getattr__" src/anndata/__init__.py src/anndata/_warnings.py`
- `rg -n "copy_on_write_X|zarr_write_format|auto_shard_zarr_v3" src/anndata/_settings.py`
- `rg -n "read_elem_lazy|chunks|OldFormatWarning|legacy" src/anndata/_io src/anndata/_io/specs/registry.py`
- `rg -n "test_backwards_compat_files|test_old_format_warning" tests`

## Suggested source entry points (function-level)
- `src/anndata/__init__.py` | `__getattr__` deprecates `anndata.__version__`
- `src/anndata/_settings.py` | `validate_zarr_write_format`, `validate_zarr_sharding` and registered options including `copy_on_write_X`
- `src/anndata/_io/specs/registry.py` | `read_elem_lazy`, `read_elem_partial`
- `src/anndata/_io/zarr.py` | `read_zarr`, `write_zarr` and old-format warning path
- `src/anndata/_io/h5ad.py` | `read_h5ad`, `write_h5ad` and legacy dataframe readers
- `src/anndata/_warnings.py` | `OldFormatWarning`, `ExperimentalFeatureWarning`, `warn`
- `tests/test_io_backwards_compat.py` | `test_backwards_compat_files`, `test_no_diff`
- `tests/test_io_warnings.py` | `test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`
- `tests/lazy/test_read.py` | lazy-read regression coverage used by 0.12.x changes

## Function probes
```bash
rg -n "def __getattr__\\(|__version__|OldFormatWarning" src/anndata/__init__.py src/anndata/_warnings.py
rg -n "def (validate_zarr_write_format|validate_zarr_sharding)\\(|copy_on_write_X" src/anndata/_settings.py
rg -n "def (read_elem_lazy|read_elem_partial)\\(" src/anndata/_io/specs/registry.py
rg -n "def (read_zarr|write_zarr|read_h5ad|write_h5ad)\\(" src/anndata/_io/zarr.py src/anndata/_io/h5ad.py
rg -n "def (test_backwards_compat_files|test_no_diff|test_old_format_warning_thrown|test_old_format_warning_not_thrown)\\(" tests/test_io_backwards_compat.py tests/test_io_warnings.py
```

## Validation checkpoint
- For each release-note bullet you use, confirm at least one matching source or test probe hit from this map.
