# anndata source map: Typing

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
- `Index1D`
- `Index`
- `AxisStorable`
- `RWAble`
- `Protocol`
- `read_elem`
- `write_elem`

## Fast source navigation
- `rg -n "^type (Index1D|Index|AxisStorable|RWAble)" src/anndata/typing.py`
- `rg -n "class .*Protocol|ReadCallback|WriteCallback|StorageType" src/anndata/_types.py src/anndata/types.py`
- `rg -n "def (read_elem|write_elem|read_elem_lazy)\\(|StorageType" src/anndata/_io/specs/registry.py src/anndata/io.py`

## Suggested source entry points (function-level)
- `src/anndata/typing.py` | type aliases `Index1D`, `Index`, `AxisStorable`, `RWAble`
- `src/anndata/_types.py` | protocol contracts `_ReadInternal`, `Read`, `ReadLazy`, `Write`, `ReadCallback`, `WriteCallback`
- `src/anndata/types.py` | public protocols `ExtensionNamespace`, `SupportsArrayApi`
- `src/anndata/_core/anndata.py` | `AnnData.__getitem__` signatures and index behavior boundary
- `src/anndata/_io/specs/registry.py` | `read_elem`, `read_elem_lazy`, `write_elem` typing boundary
- `src/anndata/io.py` | exported IO entry points used in public annotations

## Function probes
```bash
rg -n "^type (Index1D|Index|AxisStorable|RWAble)" src/anndata/typing.py
rg -n "class (Dataset2DIlocIndexer|_ReadInternal|Read|ReadLazy|Write|ReadCallback|WriteCallback)" src/anndata/_types.py
rg -n "class (ExtensionNamespace|SupportsArrayApi)" src/anndata/types.py
rg -n "def __getitem__\\(" src/anndata/_core/anndata.py
rg -n "def (read_elem|read_elem_lazy|write_elem)\\(" src/anndata/_io/specs/registry.py
```

## Validation checkpoint
- Confirm proposed annotations match both `typing.py` aliases and runtime indexing behavior (`AnnData.__getitem__`) before finalizing recommendations.
