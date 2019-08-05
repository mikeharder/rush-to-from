# Repro
Consider a dependency graph where `B` depends on `A`, and `D` depends on both `B` and `C`:

```
A -> B -> D
     C -> D
```

Say I am making changes to `B`, and want to verify that `B` and all its downstream dependencies (`D`) can build correctly.  I use the following command:

```
rush build --to B --from B
```

## Expected
Rush should build all projects, including `C`.  `D` is downstream of `B` so it must be built, and `C` is upstream of `D` so it must also be built.

## Actual
Rush does not build `C`.
