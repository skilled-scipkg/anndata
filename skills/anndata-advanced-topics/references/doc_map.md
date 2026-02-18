# anndata documentation map: Advanced Topics

Generated from documentation roots:
- `docs`
- `docs/tutorials`
- `tests`
- `src/anndata/tests`

Total docs grouped in this topic: 8

## Start from `skills/`
```bash
ROOT="$(git rev-parse --show-toplevel)"
cd "$ROOT"
```

## Verify mapped docs exist
```bash
for p in docs/benchmarks.md docs/concatenation.rst docs/fileformat-prose.md docs/interoperability.md; do
  test -f "$p" || echo "missing: $p"
done
```

## File inventory
- `docs/benchmarks.md` | title: Benchmarks | headings: Benchmarks; benchmark-read-write
- `docs/concatenation.rst` | title: Concatenation | headings: Concatenation; Inner and outer joins; Annotating data source (`label`, `keys`, and `index_unique`)
- `docs/tutorials/index.md` | title: Tutorials | headings: Tutorials; zarr-v3
- `docs/fileformat-prose.md` | title: On-disk format | headings: On-disk format; Elements; Element Specification
- `docs/index.md` | title: Latest additions | headings: Latest additions; ```{include} ../README.md; references
- `docs/interoperability.md` | title: Interoperability | headings: Interoperability; R; Julia
- `docs/_key_contributors.rst` | title: Key Contributors | headings: (no heading extracted)
- `docs/references.rst` | title: References | headings: References
