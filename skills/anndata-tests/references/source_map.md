# anndata source map: Tests

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
- `backwards_compat`
- `OldFormatWarning`
- `archives`
- `read_h5ad`
- `read_zarr`
- `h5diff`

## Fast source navigation
- `rg -n "backwards_compat|archive|h5diff" tests/test_io_backwards_compat.py tests/data/archives/readme.md`
- `rg -n "OldFormatWarning|FutureWarning" tests/test_io_warnings.py src/anndata/_warnings.py`
- `rg -n "read_h5ad|read_zarr|ZipStore" tests/test_readwrite.py src/anndata/_io`

## Suggested source entry points (function-level)
- `tests/test_io_backwards_compat.py` | `read_archive`, `test_backwards_compat_files`, `test_no_diff`
- `tests/test_io_warnings.py` | `test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`
- `tests/test_readwrite.py` | `test_readwrite_roundtrip`, `test_readwrite_equivalent_h5ad_zarr`, `test_zarr_compression`
- `tests/data/archives/readme.md` | fixture policy and support matrix
- `src/anndata/_io/h5ad.py` | `read_h5ad`, `write_h5ad`
- `src/anndata/_io/zarr.py` | `read_zarr`, `write_zarr`
- `src/anndata/_io/utils.py` | `report_read_key_on_error`, `_read_legacy_raw`
- `src/anndata/_warnings.py` | `OldFormatWarning`, `warn`

## Function probes
```bash
rg -n "def (read_archive|test_backwards_compat_files|test_no_diff)\\(" tests/test_io_backwards_compat.py
rg -n "def (test_old_format_warning_thrown|test_old_format_warning_not_thrown)\\(" tests/test_io_warnings.py
rg -n "def (test_readwrite_roundtrip|test_readwrite_equivalent_h5ad_zarr|test_zarr_compression)\\(" tests/test_readwrite.py
rg -n "def (read_h5ad|write_h5ad|read_zarr|write_zarr)\\(" src/anndata/_io/h5ad.py src/anndata/_io/zarr.py
rg -n "def (report_read_key_on_error|_read_legacy_raw|warn)\\(|class OldFormatWarning" src/anndata/_io/utils.py src/anndata/_warnings.py
```

## Validation checkpoint
- Before changing tests or serialization code, verify all function probes match and load at least one archive fixture (for example `tests/data/archives/v0.11.4/adata.h5ad`).
