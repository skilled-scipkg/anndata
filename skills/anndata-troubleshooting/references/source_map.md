# anndata source map: Troubleshooting

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
- `OldFormatWarning`
- `legacy`
- `backwards compat`
- `read_h5ad`
- `read_zarr`
- `read_elem`
- `write_elem`
- `FutureWarning`

## Fast source navigation
- `rg -n "OldFormatWarning|ExperimentalFeatureWarning|ImplicitModificationWarning" src/anndata/_warnings.py`
- `rg -n "legacy|raw|backwards compat|read_h5ad|read_zarr" src/anndata/_io src/anndata/compat`
- `rg -n "OldFormatWarning|backwards_compat|forward slash|read_elem|write_elem" tests src/anndata/_settings.py`

## Suggested source entry points (function-level)
- `src/anndata/_io/h5ad.py` | `read_h5ad`, `read_h5ad_backed`, `write_h5ad`
- `src/anndata/_io/zarr.py` | `read_zarr`, `write_zarr`, `is_group_consolidated`
- `src/anndata/_io/utils.py` | `_read_legacy_raw`, `report_read_key_on_error`, `report_write_key_on_error`
- `src/anndata/compat/__init__.py` | `_read_attr`, `_from_fixed_length_strings`, `_decode_structured_array`
- `src/anndata/_warnings.py` | `OldFormatWarning`, `warn`
- `src/anndata/_settings.py` | forward-slash and format-setting validation paths
- `tests/test_io_warnings.py` | `test_old_format_warning_thrown`, `test_old_format_warning_not_thrown`
- `tests/test_io_backwards_compat.py` | `test_backwards_compat_files`
- `tests/test_readwrite.py` | `test_read_full_io_error`, `test_readwrite_roundtrip`

## Function probes
```bash
rg -n "def (read_h5ad|read_h5ad_backed|write_h5ad|read_zarr|write_zarr|is_group_consolidated)\\(" src/anndata/_io/h5ad.py src/anndata/_io/zarr.py
rg -n "def (_read_legacy_raw|report_read_key_on_error|report_write_key_on_error)\\(" src/anndata/_io/utils.py
rg -n "def (_read_attr|_from_fixed_length_strings|_decode_structured_array)\\(" src/anndata/compat/__init__.py
rg -n "class OldFormatWarning|def warn\\(" src/anndata/_warnings.py
rg -n "def (test_old_format_warning_thrown|test_old_format_warning_not_thrown|test_backwards_compat_files|test_read_full_io_error)\\(" tests/test_io_warnings.py tests/test_io_backwards_compat.py tests/test_readwrite.py
```

## Validation checkpoint
- Reproduce with the smallest archive fixture first; if probes do not map to the observed warning/error path, expand scope only then.
