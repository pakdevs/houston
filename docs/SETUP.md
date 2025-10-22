# Setup (Windows + PowerShell + VS Code + Python)

Documenting the exact environment and steps used for the 3‑hour test so others can reproduce it.

## Summary

- OS: Windows
- Shell: PowerShell (v5.1)
- Editor: VS Code
- Python: 3.13 (project venv at `.venv/`)
- Kernel: Jupyter kernel registered as "Python (.venv) Houston"
- Key libs: pandas, numpy, jupyter, matplotlib (Agg), seaborn, requests, openpyxl, pyarrow, altair
- Project root: this folder

## 1) Install/check prerequisites

```powershell
py --version
python --version
code --version
git --version
```

If Python/Git are missing, install from python.org and git-scm.com. In the Python installer, check "Add python.exe to PATH".

## 2) Create and activate virtual environment

```powershell
py -3 -m venv .venv
.\.venv\Scripts\Activate.ps1
# If blocked, allow for this session only:
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass; .\.venv\Scripts\Activate.ps1
```

## 3) Install dependencies

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Packages are pinned in `requirements.txt`. Matplotlib uses the headless "Agg" backend in our notebooks/scripts to avoid Tk/Tcl issues.

## 4) Register the Jupyter kernel

```powershell
.\.venv\Scripts\python -m ipykernel install --user --name "houston-venv" --display-name "Python (.venv) Houston"
```

## 5) VS Code configuration

- Extensions: Python (Microsoft), Jupyter (Microsoft), Pylance (Microsoft)
- Interpreter: Ctrl+Shift+P → "Python: Select Interpreter" → choose `.venv` inside this project
- Settings: `.vscode/settings.json` points at `.venv/Scripts/python.exe` and surfaces the kernel

## 6) Folder structure (already created)

- `data/raw` — original downloads (unchanged)
- `data/processed` — cleaned/derived files
- `notebooks` — Jupyter notebooks (`01_ingest_eda.ipynb`)
- `output/charts`, `output/tables` — exported figures/tables
- `docs` — this setup doc, methods, sources, AI log, story outline

## 7) Quick smoke test

Open `notebooks/01_ingest_eda.ipynb` in VS Code, select the "Python (.venv) Houston" kernel, then Run All. Expected outputs:

- `output/tables/summary.csv`
- `output/charts/hist_*.png`
  If no CSV exists in `data/raw/`, the notebook writes a tiny sample dataset there and uses it.

## 8) Logging and reproducibility

- Document sources and access dates in `docs/SOURCES.md`
- Record methods/transformations in `docs/METHODS.md`
- Keep a timestamped work log in `docs/RUN_LOG.md`
- Commit logical changes; avoid committing large raw files

## 9) Troubleshooting

- Tk/Tcl error on Windows: notebooks/scripts set `matplotlib.use("Agg")` to render without a GUI
- Wrong kernel or interpreter: re-select `.venv` and the "Python (.venv) Houston" kernel in VS Code
- Activation blocked: use the one-line policy bypass shown above
- Missing packages: re-run `pip install -r requirements.txt`, then restart VS Code and the kernel
