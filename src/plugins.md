# Python plugins

## mypy

```toml
[tool.mypy]
exclude = "playground"
strict = true

explicit_package_bases = true
ignore_missing_imports = true
no_site_packages = true
disallow_untyped_decorators = false
pretty = true
# disable_error_code = ["attr-defined", "type-arg", "no-untyped-def"]

warn_redundant_casts = true
warn_unused_ignores = true
disallow_any_generics = false  # TODO: Enable this
check_untyped_defs = true
no_implicit_reexport = true
disallow_untyped_defs = false  # TODO: Enable this
```
