# Exams (MkDocs + Material)

## 1) Virtuálne prostredie (Windows)

V Git Bash nefunguje `source .venv/bin/activate`, lebo na Windows je aktivácia v `Scripts/`.

```bash
python -m venv .venv

# Git Bash (MINGW64):
source .venv/Scripts/activate

# PowerShell alternatíva:
# .venv\Scripts\Activate.ps1
```

Tip: `.venv` je „dot folder“, preto ho neuvidíš bez `ls -a`.

## 2) Inštalácia

```bash
pip install mkdocs-material
```

## 3) Spustenie lokálne

```bash
mkdocs serve
```

Otvor `http://127.0.0.1:8000`.

## 4) Build

```bash
mkdocs build
```

Výstup je v `site/`.

## Štruktúra

- `mkdocs.yml`
- `docs/index.md`
- `docs/1.rocnik/` a `docs/2.rocnik/` (ročníky, semestre, predmety)