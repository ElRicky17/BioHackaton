# BioHackathon — Cancer Image Classification with Deep Learning

## Project context

This project was developed during a BioHackathon. The main challenge was to build a Deep Learning model for histopathological image recognition capable of:

- Detecting the presence or absence of cancer
- Identifying the magnification level of the sample
- Classifying the type of cancer (benign or malignant)
- Identifying the type of tissue sample

The team made decisions on the computer vision model architecture, explained the biological context behind histopathological analysis, and addressed bioethical implications of handling clinical data.

---

## Dataset

**BreakHis — Breast Cancer Histopathological Database**
https://www.kaggle.com/datasets/ambarish/breakhis

The dataset contains histopathological images of breast tumors at different magnifications (40x, 100x, 200x, 400x), labeled as:

- Benign: adenosis, fibroadenoma, phyllodes tumor, tubular adenoma
- Malignant: ductal carcinoma, lobular carcinoma, mucinous carcinoma, papillary carcinoma

### Download

1. Create a Kaggle account and generate an API token from `Settings > API > Create New Token`.
2. Run:

```bash
pip install kaggle
mkdir -p ~/.kaggle && cp kaggle.json ~/.kaggle/
chmod 600 ~/.kaggle/kaggle.json
kaggle datasets download -d ambarish/breakhis
unzip breakhis.zip -d data/
```

---

## Project structure

```
Hackathon/
├── app/
│   ├── main.py           # FastAPI application
│   ├── predictor.py      # Model inference logic
│   └── static/           # Frontend assets
├── PDB/                  # Protein structure files generated with AlphaFold
├── outputs/              # Trained model checkpoints
├── train.ipynb           # Training notebook
└── requirements.txt
```

---

## Protein structure modeling (AlphaFold)

The `PDB/` folder contains `.pdb` files generated using AlphaFold in Google Colab:

- Native protein structure
- Mutated protein variant associated with the cancerous phenotype

These files can be visualized with UCSF ChimeraX or iCn3D.

---

## Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd Hackathon
```

### 2. Create and activate a virtual environment

```bash
python -m venv env

# Windows
env\Scripts\activate

# macOS / Linux
source env/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Train the model

```bash
jupyter notebook train.ipynb
```

### 5. Run the web application

The app uses FastAPI and must be launched with `uvicorn` from the project root (not from inside the `app/` folder):

```bash
uvicorn app.main:app --reload
```

Then open in your browser.

---

## Bioethical considerations

Histopathological images are sensitive clinical data and must only be used for research purposes under informed consent. Classification models do not replace professional medical diagnosis. Training data bias can affect model fairness across different patient populations. Any clinical deployment requires regulatory validation.

---

## Technologies

Python, TensorFlow / Keras, FastAPI, uvicorn, AlphaFold, Kaggle BreakHis Dataset
