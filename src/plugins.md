# Python plugins

## poetry

```bash,icon=.devicon-bash-plain
poetry init
poetry env use python3
poetry shell

poetry install  # 從現有的 pyproject.toml 或 poetry.lock 安裝
poetry install --only main --no-root

poetry add "package"
poetry add black -G dev
poetry remove "package"
poetry update "package"
poetry lock

poetry show ["package"]
poetry show --tree
poetry export -f requirements.txt -o requirements.txt
poetry export -f requirements.txt --without-hashes -o requirements.txt --only main


poetry config --list
poetry config virtualenvs.in-project true
```

## isort

## black

## ruff

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

```python,icon=.devicon-python-plain
# <https://mypy.readthedocs.io/en/latest/type_inference_and_annotations.html>
# mypy: ignore-errors
# type: ignore[attr-defined]
```

## pydantic

## orjson
