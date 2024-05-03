# Python plugins

## poetry

```bash,icon=.devicon-bash-plain
poetry init  # 初始化一個 pyproject.toml
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

```bash,icon=.devicon-bash-plain
isort .
isort . --profile black --filter-files
```

## black

```bash,icon=.devicon-bash-plain
black .
```

## ruff

```bash,icon=.devicon-bash-plain
ruff check .
```

## mypy

```toml
[tool.mypy]
plugins = ["pydantic.mypy"]
python_version = "3.12"
# mypy_path = "stubs"
strict = true
allow_untyped_calls = true  # for third party library
allow_untyped_decorators = true  # for third party library
explicit_package_bases = true
exclude = ["playground"]  # 排除哪些資料夾不檢查
follow_imports = "silent"

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

```bash,icon=.devicon-bash-plain
mypy .
mypy . --python-version=3.12
```

## pydantic

<https://docs.pydantic.dev/latest/>

## orjson

```python,icon=.devicon-python-plain
import orjson
```

## rich

<https://github.com/Textualize/rich>

```python,icon=.devicon-python-plain
from rich import print
from rich.console import Console

console = Console()
```

## icecream

```python,icon=.devicon-python-plain
ic("你要 print 的東西")
```

## pre-commit

```bash,icon=.devicon-bash-plain
# See https://pre-commit.com for more information
# See https://pre-commit.com/hooks.html for more hooks

pre-commit install         # 啟用指定的 git hook
pre-commit autoupdate      # 更新以下 repo 的版本
pre-commit run --all-files #  全檔案檢查，而不是只有被提交的檔案
pre-commit run <hook_id> --all-files #  全檔案檢查，但只檢查特定 hook
```

## commitizen

```bash,icon=.devicon-bash-plain
cz c     # update changelog
cz ch    # git commit
cz bump  # 版號升級
```

## viztracer

<https://github.com/gaogaotiantian/viztracer>

```python,icon=.devicon-python-plain
from viztracer import VizTracer

tracer = VizTracer()
tracer.start()
# Something happens here
tracer.stop()
tracer.save()

with VizTracer() as tracer:
    # Something happens here

# Jupyter
# You need to load the extension first
%load_ext viztracer

%%viztracer
# Your code after
```

## celery
