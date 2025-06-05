# 🚀 Django Project Setup with `uv`, `ruff`, and `pre-commit`

This guide walks you through setting up a new Django project using:

- [`uv`](https://github.com/astral-sh/uv) for environment and dependency management
- [`Django`](https://www.djangoproject.com/) for web development
- [`ruff`](https://github.com/astral-sh/ruff) for fast linting and formatting
- [`pre-commit`](https://pre-commit.com/) for automated code quality checks

---

## ✅ Prerequisites

- Python 3.8+
- `uv` installed

Install `uv`:

```bash
curl -Ls https://astral.sh/uv/install.sh | sh
```

---

## 🔢 Step 1: Initialize the Project with `uv`

```bash
uv init myproject
cd myproject
```

This creates:

- A project folder
- A virtual environment (`.venv`)
- A `pyproject.toml` file

---

## 🔢 Step 2: Install Django, Ruff, and Pre-commit

```bash
uv add django
uv add --dev ruff pre-commit
```

This adds:

- `django` to `[dependencies]`
- `ruff` and `pre-commit` to `[dev-dependencies]` in `pyproject.toml`

---

## 🔢 Step 3: Create Django Project and App

```bash
uv run django-admin startproject config .
uv run python manage.py startapp blog
```

Update `config/settings.py` to include the new app:

```python
INSTALLED_APPS = [
    ...
    'blog',
]
```

---

## 🔢 Step 4: Set Up `pre-commit` with `ruff`

Create a `.pre-commit-config.yaml` file:

```yaml
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.4.4  # Use the latest version
    hooks:
      - id: ruff
      - id: ruff-format
```

Install the git hooks:

```bash
uv run pre-commit install
```

Now `ruff` will automatically run on every commit.

---

## 🔢 Step 5: Run Linting and Formatting Manually (Optional)

```bash
uv run ruff .
uv run ruff format .
```

---

## 🔢 Step 6: Configure Ruff in `pyproject.toml` (Optional)

```toml
[tool.ruff]
line-length = 88
target-version = "py311"

[tool.ruff.lint]
select = ["E", "F", "I"]
```

---

## 🔢 Step 7: Apply Initial Migrations and Start Server

```bash
uv run python manage.py migrate
uv run python manage.py runserver
```

Visit http://127.0.0.1:8000/ to see your project in the browser.

---

## 🔢 Step 8: (Optional) Add Additional Developer Tools

```bash
uv add --dev black mypy django-stubs types-requests
```

Configure them in `pyproject.toml` as needed.

---

## ✅ Done!

You now have a fully functional, modern Django setup with:

- Isolated environment via `uv`
- Dependency tracking in `pyproject.toml`
- Django project scaffolded
- `ruff` for linting & formatting
- `pre-commit` enforcing clean commits

Happy building! 🚀
