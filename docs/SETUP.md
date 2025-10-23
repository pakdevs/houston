# Setup (Windows + PowerShell + VS Code + Python)

Short, reproducible steps to get this project running.

## Environment

- Windows + PowerShell (v5.1)
- VS Code
- Python 3.13 with project venv at `.venv/`
- Jupyter kernel: "Python (.venv) Houston"
- Libraries: pandas, numpy, jupyter, matplotlib (Agg), seaborn, requests, openpyxl, pyarrow, altair

## 1) Check prerequisites

```powershell
py --version
python --version
code --version
git --version
```

If missing, install Python (add to PATH during install) and Git.

## 2) Create and activate the virtual environment

```powershell
py -3 -m venv .venv
.\.venv\Scripts\Activate.ps1
# If activation is blocked, temporarily allow it for this session:
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass; .\.venv\Scripts\Activate.ps1
```

## 3) Install dependencies

```powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

Packages are listed in `requirements.txt`. Notebooks use the headless "Agg" Matplotlib backend to avoid GUI issues.

## 4) Register the Jupyter kernel

```powershell
.\.venv\Scripts\python -m ipykernel install --user --name "houston-venv" --display-name "Python (.venv) Houston"
```

## 5) VS Code configuration

- Install extensions: Python, Jupyter, Pylance (Microsoft)
- Select interpreter: Ctrl+Shift+P → "Python: Select Interpreter" → pick this project’s `.venv`
- `.vscode/settings.json` points to `.venv/Scripts/python.exe` and surfaces the kernel

## 6) Folder structure

- `data/raw` — put your original files here (CSV/XLSX)
- `data/processed` — cleaned/derived files
- `notebooks` — Jupyter notebooks (e.g., `houston.ipynb`)
- `output/charts`, `output/tables` — exported figures/tables
- `docs` — setup, methods, sources, logs

## 7) Run the EDA notebook

- Place a CSV or XLSX in `data/raw/` (required — no sample will be created)
- Open `notebooks/houston.ipynb` in VS Code
- Select the "Python (.venv) Houston" kernel and Run All
- Outputs will be saved to `output/tables/` and `output/charts/`

## 8) Troubleshooting

- Tk/Tcl errors: notebooks set `matplotlib.use("Agg")` (no GUI required)
- Wrong kernel/interpreter: reselect the project `.venv` and kernel in VS Code
- Activation blocked: use the one-line ExecutionPolicy bypass shown above
- Missing packages: `pip install -r requirements.txt`, then restart VS Code and the kernel
