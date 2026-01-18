# Exams (MkDocs + Material)

## 1) Virtuálne prostredie (Windows)

```bash
python -m venv .venv
source .venv/Scripts/activate
```

## 2) Inštalácia

```bash
pip install mkdocs-material
```

## 3) Spustenie lokálne

```bash
mkdocs serve
```
```bash
source .venv/Scripts/activate && mkdocs serve
```

Otvor `http://127.0.0.1:8000`.

## 4) Build

```bash
mkdocs build
```
```bash
source .venv/Scripts/activate && mkdocs build
```

Výstup je v `site/`.

## Štruktúra

- `mkdocs.yml`
- `docs/index.md`
- `docs/1.rocnik/` a `docs/2.rocnik/` (ročníky, semestre, predmety)
