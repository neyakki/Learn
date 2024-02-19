# Конфигурация проекта python

[Здесь](https://www.build-python-from-source.com/) можно собрать установку python

## Настройки Vs Code для Python

```json
{
    "mypy.enabled": true,
    "mypy.dmypyExecutable": "${workspaceFolder}/.venv/bin/dmypy",
    "mypy.configFile": "${workspaceFolder}/pyproject.toml",
    "bandit.args": ["--config=${workspaceFolder}/pyproject.toml"],
    "ruff.lint.args": ["--config=${workspaceFolder}/pyproject.toml"],
    "ruff.format.args": ["--config=${workspaceFolder}/pyproject.toml"],
    "[python]": {
        "editor.defaultFormatter": "charliermarsh.ruff"
    }
}
```

## Poetry

Ссылка на [документацию](https://python-poetry.org/docs/)

```bash
cache-dir = "/home/xxx/.cache/pypoetry"
experimental.system-git-client = false
installer.max-workers = null
installer.modern-installation = true
installer.no-binary = null
installer.parallel = true
virtualenvs.create = true
virtualenvs.in-project = true
virtualenvs.options.always-copy = false
virtualenvs.options.no-pip = false
virtualenvs.options.no-setuptools = false
virtualenvs.options.system-site-packages = false
virtualenvs.path = "{cache-dir}/virtualenvs"  # /home/xxx/.cache/pypoetry/virtualenvs
virtualenvs.prefer-active-python = false
virtualenvs.prompt = ".venv"
warnings.export = true
```

Динамическое [версионирование](https://pypi.org/project/poetry-dynamic-versioning/) для poetry

## Pyproject.toml

```toml
# https://python-poetry.org/docs/
[build-system]
requires = ["poetry-core>=1.0.0", "poetry-dynamic-versioning>=1.0.0,<2.0.0"]
build-backend = "poetry_dynamic_versioning.backend"

# https://github.com/mtkennerly/poetry-dynamic-versioning
[tool.poetry-dynamic-versioning]
enable = true
vcs = "git"
style = "pep440"
bump = true
dirty = true

[tool.poetry]
name = "project"
version = "0.0.0"
description = ""
authors = ["Neto42 <na011912@gmail.com>"]

[tool.poetry.dependencies]
python = "^3.10"

[tool.poetry.group.dev.dependencies]
pytest = "^8.0.1"
ruff = "^0.2.1"
mypy = "^1.8.0"
bandit = "^1.7.7"
coverage = "^7.4.1"
invoke = "^2.2.0"

# https://mypy.readthedocs.io/en/stable/
[tool.mypy]
python_version = "3.10"
exclude = [
    ".coverage_html",
    ".git",
    ".ipynb_checkpoints",
    "build",
    "dist",
    "node_modules",
    "site-packages",
    "__pycache__",
    ".mypy_cache",
    ".ruff_cache",
    ".pytest_cache",
    ".venv",
    "venv",
    ".vscode",
]
strict = true
explicit_package_bases = true

[[tool.mypy.overrides]]
module = ["requests"]
ignore_missing_imports = true

# https://mypy.readthedocs.io/en/stable/
[tool.ruff]
exclude = [
    ".coverage_html",
    ".git",
    ".ipynb_checkpoints",
    "build",
    "dist",
    "node_modules",
    "site-packages",
    "__pycache__",
    ".mypy_cache",
    ".ruff_cache",
    ".pytest_cache",
    ".venv",
    "venv",
    ".vscode",
]
line-length = 100
indent-width = 4
target-version = "py310"
namespace-packages = ["src"]

[tool.ruff.lint]
select = [
    "F",
    "W",
    "E",
    "C90",
    "I",
    "N",
    "D",
    "A",
    "B",
    "UP",
    "SLOT",
    "ARG",
    "PL",
    "RUF",
    # "SIM",
    # "DTZ",
    # "EM",
    # "G",
    # "C4",
    # "PIE",
    # "PT",
    # "T20",
    # "PTH",
]
ignore = [
    # Рекомендация ruff для фомратера
    # https://docs.astral.sh/ruff/formatter/#conflicting-lint-rules
    "W191",   # табуляция в отсупе
    "E111",   # Большой отступ
    "E114",   # Большой отступ (комментаррий)
    "E117",   # Чрезмерный отступ (комментарий)
    "D203",   # Перед строкой документации класса требуется 1 пустая строка.
    "D212",   # Многострочное резюме документации должно начинаться с первой строки.
    "D206",   # Строка документации должна иметь отступы с пробелами, а не с табуляцией.
    "D300",   # Использование """
    "D415",   # Точка в конце
    "Q",      # Кавычки
    "COM",    # Запятые
    "ISC",    # Строковое объединение
    "RUF001", # Кириллица
    "RUF002", # Кириллица
]
fixable = [
    "F",
    "W",
    "E",
    "I",
    "D",
    "B",
    "UP",
    "PL",
    "RUF",
    # "SIM",
    # "C4",
    # "PIE",
    # "PT",
    # "T20",
    # "PTH",
]
unfixable = ["ALL"]
ignore-init-module-imports = true
preview = true

[tool.ruff.lint.isort]
known-local-folder = ["src"]
required-imports = ["from __future__ import annotations"]

[tool.ruff.lint.pycodestyle]
max-doc-length = 72

[tool.ruff.lint.pydocstyle]
convention = "google"

[tool.ruff.lint.per-file-ignores]
"**/{tests,docs,tools}/*" = ["PLR6301", "PLR2004"]

[tool.ruff.format]
quote-style = "double"
indent-style = "space"
skip-magic-trailing-comma = false
docstring-code-format = true
docstring-code-line-length = 80

# https://bandit.readthedocs.io/en/latest/
[tool.bandit]
exclude_dirs = [
    ".coverage_html",
    ".eggs",
    ".git",
    ".ipynb_checkpoints",
    "build",
    "dist",
    "node_modules",
    "site-packages",
    "__pycache__",
    ".mypy_cache",
    ".ruff_cache",
    ".pytest_cache",
    ".venv",
    "venv",
    ".vscode",
    "tests",
]

# https://docs.pytest.org/en/stable/reference/reference.html#configuration-options
[tool.pytest.ini_options]
pythonpath = ". src"
testpaths = ["tests"]
console_output_style = "count"
python_files = "test_*.py"
python_classes = "Test*"
python_functions = "test_"

# https://coverage.readthedocs.io/en/7.4.1
[tool.coverage.run]
branch = true
source = ["project"]
omit = ["docs", "tests"]

[tool.coverage.report]
sort = "cover"
# Regexes for lines to exclude from consideration
exclude_also = [
    "@(abc\\.)?abstractmethod",
    "raise NotImplementedError",
    "if __name__ == .__main__.:",
]
ignore_errors = true
include_namespace_packages = true

[tool.coverage.html]
directory = ".coverage_html"
```

## Invoke

Ссылка на [документацию](https://www.pyinvoke.org/)

```python
"""
Набор функций и задач

===================================================
Author: funny-neto-code <na011912@gmail.com>
"""
from __future__ import annotations

import os

from invoke.context import Context
from invoke.tasks import task

DEFAULT_CONFIG_FILE = os.environ.get("CONFIG_FILE", "pyproject.toml")
DEFAULT_REMOVE_FILES = ["dist"]


@task
def check(c: Context) -> None:
    """Проверка проекта"""
    c.run("poetry check", echo=True)


@task(pre=[check])
def lint(
    c: Context,
    file: str = ".",
    config_file: str = DEFAULT_CONFIG_FILE,
    silent: bool = False,
) -> None:
    """Проверка линетром"""
    cmd = f"ruff --config={config_file}"

    if silent is True:
        c.run(f"{cmd} --silent {file}", echo=True)
        return

    c.run(f"{cmd} {file}", echo=True)


@task(pre=[check])
def format(  # noqa: A001
    c: Context,
    file: str = ".",
    config_file: str = DEFAULT_CONFIG_FILE,
    silent: bool = False,
) -> None:
    """Форматирование файлов"""
    cmd_fix = f"ruff --fix --config={config_file}"
    cmd_format = f"ruff format --config={config_file}"

    if silent is True:
        c.run(f"{cmd_fix} --silent {file}", echo=True)
        c.run(f"{cmd_format} --silent {file}", echo=True)
        return

    c.run(f"{cmd_fix} {file}", echo=True)
    c.run(f"{cmd_format} {file}", echo=True)


@task(pre=[check])
def clean(c: Context, extend: str | None = None) -> None:
    """Очистка проекта"""
    _remove_file = DEFAULT_REMOVE_FILES.copy()

    if extend:
        _remove_file.extend(extend)

    c.run(f"rm -rf {' '.join(_remove_file)}", echo=True)


@task(pre=[check, clean])
def build(c: Context) -> None:
    """Сборка проекта"""
    c.run("poetry build", echo=True)


@task(name="test")
def run_test(
    c: Context,
    file: str = ".",
    doctest: bool = False,
) -> None:
    """Запусков тестов"""
    cmd = f"coverage run -m pytest -v {file}"

    if doctest:
        c.run(f"{cmd} --doctest-modules --doctest-continue-on-failure", echo=True)

    c.run(cmd, echo=True)


@task(pre=[run_test])
def report(c: Context) -> None:
    """Создание в консоли отчета покрытия кода тестами"""
    c.run("coverage report -m", echo=True)


@task(pre=[run_test])
def lcov(c: Context) -> None:
    """Создание lcov файла"""
    c.run("coverage lcov", echo=True)


@task(pre=[run_test])
def html(c: Context) -> None:
    """Создание HTML отчета покрытия кода тестами"""
    c.run("coverage html", echo=True)
```
