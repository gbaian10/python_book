# Python plugins

## mypy

```toml
[tool.mypy]
exclude = ["playground"]
strict = true
disallow_untyped_decorators = false
disallow_any_generics = false  # TODO: Enable this
check_untyped_defs = true
no_implicit_reexport = true
disallow_untyped_defs = false  # TODO: Enable this

explicit_package_bases = true
ignore_missing_imports = true
no_site_packages = true
pretty = true
# disable_error_code = ["attr-defined", "type-arg", "no-untyped-def"]
```

```python
# <https://mypy.readthedocs.io/en/latest/type_inference_and_annotations.html>
# mypy: ignore-errors
# type: ignore[attr-defined]
```
