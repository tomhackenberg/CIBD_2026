# ADS & Marketing — Block 2

Course notebooks for Block 2. Each week has its own folder. Notebooks are written in Quarto and run Python and R side by side.

---

## Setup — do this once at the start of the block

### 1. Install `uv`

`uv` manages your Python environment. It is a single install and replaces pip, venv, and pyenv in one go.

**Mac / Linux** — run in a terminal:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows** — run in PowerShell:
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Close and reopen your terminal after installing so `uv` is on your PATH.

---

### 2. Clone the repo

```bash
git clone https://github.com/yourname/ads-marketing-block2
cd ads-marketing-block2
```

---

### 3. Create the Python environment

```bash
uv sync
```

This reads `pyproject.toml`, installs the correct Python version if you don't have it, creates a `.venv/` folder, and installs all packages. It takes about 30 seconds the first time.

---

### 4. Install the R packages (once)

Open R or the R console in RStudio / Positron and run:

```r
install.packages("renv")  # skip if you already have it
renv::restore(prompt = FALSE)
```

---

### 5. Open a notebook

```bash
quarto preview week09/week09_notebook.qmd
```

Quarto reads `.venv/bin/python` from `_quarto.yml` automatically — no activation step needed.

---

## Week by week

| Week | Topic | Folder |
|------|-------|--------|
| 9 | ML basics + prediction vs. causation | `week09/` |
| 11 | FWL theorem & Double ML | `week11/` |
| 12 | DML in practice | `week12/` |
| 15 | CATE & heterogeneity | `week15/` |

Lecture slides (`.qmd`) and optional notebooks are in each week's folder. Rendered HTML versions of all notebooks are posted on Canvas for students who prefer to read without running code.

---

## Updating

When new notebooks are added during the block, pull the latest and re-sync:

```bash
git pull
uv sync
```

`uv sync` is fast — it only installs anything new, skips everything already present.

---

## Troubleshooting

**`uv: command not found` after installing**
Close and reopen your terminal. If it still fails, add `~/.cargo/bin` to your PATH.

**Quarto uses the wrong Python**
Make sure you are running `quarto` from the repo root folder (where `_quarto.yml` lives). The config file points Quarto at `.venv/bin/python` — it only takes effect from the project root.

**R packages fail to install**
Try the manual fallback:
```r
install.packages(c("dagitty", "ggdag", "ggplot2"))
```
Versions may differ slightly but the notebooks will still run.

**Anything else**
Post in the course channel on Teams. Include the full error message and which operating system you are on.
