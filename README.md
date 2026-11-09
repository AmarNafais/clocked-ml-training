# Clocked – Attendance Fraud Detection with a Variational Autoencoder

This repository contains the development notebooks for the **Clocked** attendance fraud detection model.

The project:

- builds a small **Variational Autoencoder (VAE)** that learns normal attendance behaviour and flags anomalies using reconstruction error
- compares the VAE against a **One-Class SVM** baseline
- tests whether **pretraining on public datasets** (UCI Absenteeism at Work, CERT r4.2, and a manufacturing attendance dataset) improves the Clocked VAE

> **Note:** The datasets are **not** stored in this repository. You must download them from OneDrive and place them in the correct folders before running the notebooks (see [Dataset setup](#dataset-setup)).

---

## Repository structure

```
.
├── clocked model creation and training/
│   ├── vae model creation.ipynb
│   └── both models comparison.ipynb
├── absenteeism pretraining/
│   └── absenteeism vs clocked pretraining.ipynb
├── cert r4.2 pretraining/
│   └── cert r4.2 vs clocked pretraining.ipynb
└── manufacturing pretraining/
    └── manufacturing vs clocked pretraining.ipynb
```

| Folder | Notebook | Purpose |
|---|---|---|
| `clocked model creation and training` | `vae model creation.ipynb` | Trains, tests and saves the deployable Clocked VAE |
| `clocked model creation and training` | `both models comparison.ipynb` | Compares the VAE with a One-Class SVM baseline |
| `absenteeism pretraining` | `absenteeism vs clocked pretraining.ipynb` | Clocked-only VAE vs UCI-pretrained VAE |
| `cert r4.2 pretraining` | `cert r4.2 vs clocked pretraining.ipynb` | Clocked-only VAE vs CERT r4.2-pretrained VAE |
| `manufacturing pretraining` | `manufacturing vs clocked pretraining.ipynb` | Clocked-only VAE vs manufacturing-pretrained VAE |

---

## Dataset setup

### 1. Download the data

All datasets are available in this OneDrive folder:

**👉 [Download datasets from OneDrive](https://nibm-my.sharepoint.com/:f:/g/personal/kic-bsccsai-251p-051_student_nibm_lk/IgCoSikszBMwQ4Zi1UL2YPilAcY9kQgCe4__YShByvS5XB8?e=4PoLWY)**

The OneDrive folder uses **the same folder structure as this repository**. Each folder contains the data files for the notebook(s) in that folder.

### 2. Place the files in the matching folders

Each notebook loads its data from **its own folder** (the same folder the `.ipynb` file is in). Copy every file from a OneDrive folder into the folder with the same name in this repository.

| Repository folder | Files required |
|---|---|
| `clocked model creation and training/` | `unified_attendance_1250.csv` |
| `absenteeism pretraining/` | `unified_attendance_1250.csv`, `Absenteeism_at_work.csv` |
| `cert r4.2 pretraining/` | `unified_attendance_1250.csv`, `logon.csv`, `insiders.csv` |
| `manufacturing pretraining/` | `unified_attendance_1250.csv`, `manufacturingdata3.xlsx` |

> ⚠️ `unified_attendance_1250.csv` (the Clocked dataset) is required in **all four folders**. Make sure each folder has its own copy.
>
> ⚠️ The manufacturing dataset is an **Excel file** (`.xlsx`), not a CSV.
>
> ⚠️ Do **not** rename the files. The notebooks look for these exact file names.

### 3. Check your folder layout

Once the files are in place, the project should look like this:

```
.
├── clocked model creation and training/
│   ├── vae model creation.ipynb
│   ├── both models comparison.ipynb
│   └── unified_attendance_1250.csv
├── absenteeism pretraining/
│   ├── absenteeism vs clocked pretraining.ipynb
│   ├── unified_attendance_1250.csv
│   └── Absenteeism_at_work.csv
├── cert r4.2 pretraining/
│   ├── cert r4.2 vs clocked pretraining.ipynb
│   ├── unified_attendance_1250.csv
│   ├── logon.csv
│   └── insiders.csv
└── manufacturing pretraining/
    ├── manufacturing vs clocked pretraining.ipynb
    ├── unified_attendance_1250.csv
    └── manufacturingdata3.xlsx
```

If a file is missing or in the wrong folder, the notebook stops with a `FileNotFoundError`.

---

## Environment setup

The notebooks were developed with **Python 3.14**. Python 3.10 or newer should also work.

```bash
# create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# install dependencies
pip install numpy pandas matplotlib scikit-learn torch openpyxl jupyter
```

`openpyxl` is required to read the manufacturing `.xlsx` file.

---

## Running the notebooks

Open Jupyter from the repository root:

```bash
jupyter notebook
```

Then run each notebook from top to bottom (**Kernel → Restart & Run All**).

> **Important:** Jupyter must use the notebook's own folder as its working directory, because the data paths are relative. This is the default when you open a notebook through Jupyter or VS Code.

Suggested order:

1. `clocked model creation and training/vae model creation.ipynb`
2. `clocked model creation and training/both models comparison.ipynb`
3. Any of the three pretraining notebooks (they are independent of each other):
   - `absenteeism pretraining/absenteeism vs clocked pretraining.ipynb`
   - `cert r4.2 pretraining/cert r4.2 vs clocked pretraining.ipynb`
   - `manufacturing pretraining/manufacturing vs clocked pretraining.ipynb`

> The CERT `logon.csv` file is large (~56 MB), so the CERT notebook takes longer to load.

---

## Generated outputs

The following files are **created by the notebooks**. You do not need to download them.

| Notebook | Output |
|---|---|
| `vae model creation.ipynb` | `clocked_vae_output/clocked_vae_bundle.pt`, `clocked_vae_metadata.json`, `clocked_vae_test_results.csv` |
| `absenteeism vs clocked pretraining.ipynb` | `uci_absenteeism_pretraining_comparison.csv` |
| `manufacturing vs clocked pretraining.ipynb` | `manufacturing_pretraining_comparison.csv` |

---

## Dataset sources

- **Clocked attendance dataset** – `unified_attendance_1250.csv`, created for this project.
- **UCI Absenteeism at Work** – UCI Machine Learning Repository.
- **CERT Insider Threat Dataset r4.2** – Carnegie Mellon University, Software Engineering Institute (`logon.csv` and the `insiders.csv` answer key).
- **Manufacturing employee attendance dataset** – `manufacturingdata3.xlsx`, a public research dataset.
