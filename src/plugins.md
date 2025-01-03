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

## uv

```bash,icon=.devicon-bash-plain
uv init
uv python install 3.13  # https://docs.astral.sh/uv/getting-started/features/#python-versions
uv python pin 3.13  # 將專案的 python 版本固定
uv venv  # 建立虛擬環境
uv run main.py  # 可以在不進入虛擬環境的情況下執行指令

uv add pydantic pydantic-settings
uv add --dev ruff  # 同 --group dev
uv add --group test pytest
uv remove pydantic
uv remove --group test pytest

uv lock  # 根據 pyproject.toml 創建/更新 lockfile，但只要 uv.lock 符合目前的安裝條件，則不會顯式升級套件
uv lock --locked # 檢查 lockfile 是否是最新的 (也可以使用 --check)
uv lock --upgrade-package pydantic  # 升級指定 package
uv lock --upgrade  # 升級所有 package。類似 poetry update，但不會更新到環境內，只會更新 uv.lock 檔

uv sync  # 如果 lockfile 不存在，會安裝最新且符合條件的套件，相當於 poetry install + poetry update
uv sync --group test  # 額外安裝 test group 的套件
uv sync --all-groups  # 額外安裝所有 group 的套件
uv sync --frozen  # 不會更新 lockfile，而是根據 uv.lock 來安裝套件。相當於 poetry install，但如果 lock 檔案不存在會報錯
uv sync --frozen --all-extras


uv tree
```

```toml
[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.hatch.build.targets.wheel]
packages = ["your_package_path"]
```

## pyenv

```bash,icon=.devicon-bash-plain
pyenv --version  # 查看 pyenv 版本
pyenv versions   # 列出所有已安裝的 python 版本 (如果該資料夾下有 .python-version 檔案，會使用其指定的版本，否則使用全域設定)
pyenv global system  # 切換全域設定到系統 python 版本
pyenv global 3.13.1  # 切換全域設定到指定 python 版本
pyenv local 3.12.7  # 將當前目錄切換到指定 python 版本，並寫入 .python-version 檔案內

pyenv install --list  # 列出所有可安裝的 python 版本
pyenv uninstall 3.13.0
pyenv install 3.13.1
```

### update pyenv

```bash,icon=.devicon-bash-plain
cd ~/.pyenv
git pull
```

## pipx

```bash,icon=.devicon-bash-plain
pipx list  # 列出目前安裝的套件
pipx upgrade <package>  # 升級指定套件
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

no_site_packages = true
ignore_missing_imports = true
pretty = true
# disable_error_code = ["attr-defined", "type-arg", "no-untyped-def"]

[[tool.mypy.overrides]]
module = ["app.config.pydantic_config", "app.middleware.*", "app.models._settings_model"]
allow_subclassing_any = true  # for pydantic

[[tool.mypy.overrides]]
module = "tests.*"
allow_any_generics = true
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

## pydantic-settings

<https://docs.pydantic.dev/latest/concepts/pydantic_settings/>

## orjson

```python,icon=.devicon-python-plain
import orjson
```

## rich

<https://github.com/Textualize/rich>

```python,icon=.devicon-python-plain
from rich import print
from rich.console import Console

print()
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

<https://commitizen-tools.github.io/commitizen/>

```bash,icon=.devicon-bash-plain
cz c     # update changelog
cz ch    # git commit
cz bump  # 版號升級
```

```toml
[tool.commitizen]
name = "cz_conventional_commits"
version_provider = "poetry"
update_changelog_on_bump = true
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

<https://docs.celeryq.dev/en/stable/>

<https://github.com/celery/celery>

## locust

<https://locust.io/>

<https://github.com/locustio/locust>

## loguru

<https://loguru.readthedocs.io/en/stable/>

<https://github.com/Delgan/loguru>

## streamlit

<https://docs.streamlit.io/>

<https://github.com/streamlit/streamlit>

## jellyfish

<https://jamesturk.github.io/jellyfish/>

<https://github.com/jamesturk/jellyfish>
