# 04: Data Science Best Practices

## 1. Jupyter Notebook Hygiene

Jupyter notebooks are powerful but they are also notorious for creating noisy diffs. Raw `.ipynb` files often include:

- cell outputs
- execution counts
- image data
- large metadata blobs
- hidden state from previous runs

These details make Git history noisy and can hide the actual code changes.

### Use `nbstripout`

Install it:

```bash
pip install nbstripout
```

To strip outputs from all notebooks in the repo:

```bash
nbstripout --install
```

This adds a Git filter that automatically strips output before commit. It is especially useful in data science clubs where multiple members run notebooks differently.

### Verify behavior

```bash
git status
```

After saving a notebook and running `git add`, the notebook diff should mostly reflect code changes rather than generated outputs.

### Recommended notebook workflow

- Keep notebooks for exploration, not final production logic.
- Move reusable code into scripts or modules.
- Use clean, clear markdown headings.
- Prefer `nbstripout` and clean kernel state before committing.

## 2. Data and Model Artifacts Should Not Live in Git

Large files can make a repository slow, difficult to push, and expensive to clone. In data science, avoid committing things like:

- `.csv`
- `.parquet`
- `.feather`
- `.h5`
- `.pt`
- `.pth`
- `.onnx`
- `.pkl`
- `.bin`
- `.safetensors`

### Better storage options

- DVC for versioning large data and model artifacts
- Git LFS for large binary files
- AWS S3 or Azure Blob Storage for shared datasets
- Hugging Face Hub for model weights and public assets

### Git LFS example

```bash
git lfs install
git lfs track "*.csv" "*.parquet" "*.pt" "*.onnx"
git add .gitattributes
```

This tells Git to store large files efficiently using LFS pointers instead of the full binary contents.

### DVC example

```bash
dvc init
dvc add data/raw/train.csv
```

Then commit the `.dvc` file and use a remote storage backend:

```bash
dvc remote add -d storage s3://my-bucket/dvc-store
```

This is a good choice when you need reproducible, trackable datasets without bloating Git history.

## 3. Secrets Management with `.env`

Never hardcode secrets such as:

- API tokens
- database URIs
- credentials
- private keys
- cloud access tokens

### Recommended approach

Create a `.env` file locally:

```dotenv
API_KEY=your_api_token_here
DATABASE_URL=postgresql://user:pass@host:5432/dbname
```

Then load it in Python:

```python
from dotenv import load_dotenv
import os

load_dotenv()
api_key = os.getenv("API_KEY")
```

### Always keep `.env` out of version control

Add these protections to your `.gitignore`:

```gitignore
.env
.env.*
!.env.example
credentials.json
*.pem
```

### Verify it is ignored

```bash
git check-ignore -v .env
```

If it prints a matching ignore rule, the file is protected. Basic safety rule: if a secret is needed to run a project, it should be sourced externally, not committed.

### Example `.env.example`

```dotenv
API_KEY=your_api_key_here
DATABASE_URL=postgresql://user:password@localhost:5432/app_db
```

This gives teammates a template without exposing real credentials.

## 4. Reproducibility and Environment Tracking

Data science work is only reproducible if the environment is described.

### Common options

- `requirements.txt` for simple Python projects
- `pyproject.toml` for more structured Python packaging
- `environment.yml` for Conda users

### Example requirements.txt

```txt
pandas==2.2.2
numpy==1.26.4
scikit-learn==1.4.2
python-dotenv==1.0.1
```

### Example environment.yml

```yaml
name: ds-club
channels:
  - conda-forge
  - defaults
dependencies:
  - python=3.11
  - pandas
  - numpy
  - scikit-learn
  - jupyter
  - python-dotenv
```

## 5. Recommended Data Science Repo Hygiene

Use this checklist before every commit:

- [ ] Notebook outputs removed or stripped
- [ ] Large data files excluded from Git
- [ ] Models and checkpoints stored outside Git
- [ ] Secrets stored in `.env` only
- [ ] `.env` listed in `.gitignore`
- [ ] Reproducible environment described in config files
- [ ] README updated for setup and usage

## 6. Example `.gitignore` Additions

```gitignore
# Environment variables
.env
.env.local
.env.*

# Data assets
*.csv
*.parquet
*.h5
*.feather

# Models
*.pt
*.pth
*.onnx
*.pkl
*.bin
```

## 7. Summary

Strong Git hygiene in data science is about protecting your team from accidental leaks, noisy diffs, and slow repositories. The combination of notebook stripping, external storage for data and models, secret management, and environment tracking creates a reliable foundation for reproducible collaboration.

The next resource list is in [05: Interactive Resources](./05-interactive-resources.md).
