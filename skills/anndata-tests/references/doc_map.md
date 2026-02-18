# anndata documentation map: Tests

Generated from documentation roots:
- `docs`
- `docs/tutorials`
- `tests`
- `src/anndata/tests`

Total docs grouped in this topic: 3

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

## Verify mapped docs exist
```bash
for p in tests/data/archives/readme.md tests/data/archives/v0.11.4/readme.md tests/data/archives/v0.5.0/readme.md; do
  test -f "$p" || echo "missing: $p"
done
```

## File inventory
- `tests/data/archives/readme.md` | title: archives | headings: archives; Directories
- `tests/data/archives/v0.11.4/readme.md` | title: adata.write_h5ad("tests/data/archives/v0.11.4/adata.h5ad")' | headings: adata.write_h5ad("tests/data/archives/v0.11.4/adata.h5ad")'
- `tests/data/archives/v0.5.0/readme.md` | title: Readme | headings: (no heading extracted)
