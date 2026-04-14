# Causal ML — Block 2

Course notebooks for Block 2. Each week has its own folder. Notebooks are written in Quarto and run Python side by side.

---

## Setup — do this once at the start of the block

### 1. Install `uv`

`uv` manages your Python environment — it replaces pip, venv, and pyenv in one go.

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
git clone https://github.com/tomhackenberg/CIBD_2026
cd CIBD_2026
```

---

### 3. Create the Python environment

```bash
uv sync
```

This reads `pyproject.toml`, installs the correct Python version, creates a `.venv/` folder, and installs all packages. Takes about 30 seconds the first time.

> **If `uv sync` hangs or fails:** pause OneDrive/Google Drive syncing, close VS Code, disconnect VPN, then try again. These tools can interfere with environment creation.

---

### 4. Install the R packages (once)

Open R, RStudio, or Positron and run:

```r
install.packages("renv")  # skip if you already have it
renv::restore(prompt = FALSE)
```

> **If packages fail to install**, try the manual fallback:
> ```r
> install.packages(c("dagitty", "ggdag", "ggplot2"))
> ```
> Versions may differ slightly but the notebooks will still run.

---

### 5. Preview a notebook

```bash
uv run quarto preview week_09_ML_vs_Causal/week09_notebook.qmd
```

The `uv run` prefix ensures Quarto uses the course environment. **Always use `uv run quarto ...`**, not `quarto ...` directly.

This opens a rendered HTML view in your browser — that is the intended output. To **edit and run cells interactively** (like you would in a jupyter notebook), open the `.qmd` file in VS Code with the [Quarto extension](https://marketplace.visualstudio.com/items?itemName=quarto.quarto) installed.

---

### 6. Updating during the block

When new notebooks are added, pull and re-sync:

```bash
git pull
uv sync
```

`uv sync` is fast — it only installs anything new.

---

## Week by week

| Week | Topic | Folder |
|------|-------|--------|
| 9 | ML basics + prediction vs. causation | `week_09_ML_vs_Causal/` |
| 11 | FWL theorem & Double ML | `week_11_FWL_Theorem/` |
| 12 | DML in practice | `week_12_DML/` |
| 15 | CATE & heterogeneity | `week_15_CATE_Marketing/` |

Rendered HTML versions of all notebooks are posted on Canvas if you prefer to read without running code.

---

## Troubleshooting

**`ModuleNotFoundError: No module named 'numpy'` (or any package)**  
Quarto is using the wrong Python. Make sure you are running `uv run quarto preview ...`, not `quarto preview ...`.

**`uv sync` hangs or fails**  
Pause cloud sync tools (OneDrive, Google Drive, Dropbox), close VS Code, and disconnect VPN. Then try again.

**`uv: command not found` after installing**  
Close and reopen your terminal. If it still fails, add `~/.local/bin` (Mac/Linux) or `%USERPROFILE%\.local\bin` (Windows) to your PATH.

**`(base)` or `(venv)` appears in your terminal**  
A conda or virtual environment is active and may interfere. Deactivate it first:
```bash
conda deactivate   # if using conda
deactivate         # if using a plain venv
```
Repeat until the prefix is gone, then run `uv sync`.

**VS Code uses the wrong Python kernel**  
Click the kernel selector in the top-right corner of the editor and choose the interpreter at `.venv/bin/python` (Mac/Linux) or `.venv\Scripts\python.exe` (Windows). Run `uv sync` first if it doesn't appear.

**DeprecationWarnings about `asyncio` on Windows**  
These are from Quarto's internals — not an error. Your notebook will still run. Ignore them.

**Anything else**  
Contact me via email (see Canvas). Copy-paste the full error message (not a screenshot) and include your operating system.
