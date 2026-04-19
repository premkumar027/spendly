# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

**Spendly** is a Flask-based expense tracker web app for tracking expenses in Indian Rupees (₹). This is an educational/incremental project where features are built step-by-step (Steps 1–9 as noted in `app.py` route placeholders).

## Setup & Running

```bash
source venv/bin/activate
pip install -r requirements.txt
python app.py
```

App runs at `http://localhost:5001` with debug mode enabled.

## Running Tests

```bash
pytest                        # run all tests
pytest tests/test_foo.py      # run a single test file
pytest -k "test_name"         # run a specific test by name
```

Testing uses `pytest` + `pytest-flask`. No test files exist yet — they are added incrementally as features are implemented.

## Architecture

- **`app.py`** — Flask app entry point; defines all routes. Currently implements GET routes for static/auth pages; stub routes return plain strings and are labeled with their target step number.
- **`database/db.py`** — SQLite database module (stub). Must implement `get_db()` (connection with `row_factory=sqlite3.Row` and `PRAGMA foreign_keys = ON`), `init_db()` (CREATE TABLE IF NOT EXISTS), and `seed_db()` (sample data). The `.db` file is created at runtime and is gitignored.
- **`templates/`** — Jinja2 templates; `base.html` defines the shared layout (navbar, footer, font imports). All page templates extend it using `{% block title %}`, `{% block content %}`, and optionally `{% block head %}`/`{% block scripts %}`.
- **`static/css/style.css`** — Single stylesheet for all pages.
- **`static/js/main.js`** — Placeholder for client-side JS.

## Incremental Step Map

| Step | Feature |
|------|---------|
| 1 | Database setup (`database/db.py`) |
| 2 | User registration (POST `/register`) |
| 3 | Login / logout / session management |
| 4 | Profile page |
| 5–6 | Expense listing / dashboard |
| 7 | Add expense |
| 8 | Edit expense |
| 9 | Delete expense |

## Key Conventions

- Routes follow REST-like URL patterns: `/expenses/add`, `/expenses/<id>/edit`, `/expenses/<id>/delete`.
- All monetary values are in Indian Rupees (₹).
- The virtual environment (`venv/`) is gitignored; always activate before running.
