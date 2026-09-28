# FitRank

FitRank is an NLP web app that screens a resume against a job description and builds a tailored resume for that job.

It extracts skills, experience, and education from unstructured text, scores how well a candidate matches a role, and can draft a formatted resume (with or without a photo) that you can preview, edit, and download as a PDF.

## Features

- **Screen** — paste or upload a resume and a job description (TXT, PDF, or DOCX). Get a match score, required-skill coverage, and a gap report (matched vs missing skills).
- **Resume builder** — paste a job description (and optionally your current resume). Choose a **with photo** or **without photo** layout, edit the preview, and download a PDF.
- The builder uses skills from the job description. It keeps your real experience when you provide a resume. It does not invent jobs.

Match score weights:

```
0.65 skill coverage + 0.18 TF-IDF + 0.12 education + 0.05 preferred
```

## Requirements

- Python 3.10 or newer
- pip

On Windows, if `pip.exe` or `streamlit.exe` is blocked, use `python -m pip` and `python -m streamlit`.

## Setup and run (local)

1. Open a terminal in this project folder.

2. Create and activate a virtual environment (recommended):

```bash
python -m venv .venv
```

Windows PowerShell:

```bash
.\.venv\Scripts\Activate.ps1
```

macOS / Linux:

```bash
source .venv/bin/activate
```

3. Install dependencies:

```bash
python -m pip install -r requirements.txt
```

4. (Optional) Download the Kaggle resume corpus. The Screen and Resume builder pages do **not** need this:

```bash
python load_kaggle.py
```

5. Start the app:

```bash
python -m streamlit run app.py
```

6. Open the URL Streamlit prints, usually [http://localhost:8501](http://localhost:8501).

### CLI (optional)

```bash
python cli.py --resume your_resume.txt --jd job.txt
```

## Project layout

```
app.py                 Streamlit UI (Screen + Resume builder)
cli.py                 score a resume file from the terminal
load_kaggle.py         optional Kaggle corpus download
requirements.txt       Python packages
.streamlit/config.toml light theme
src/preprocess.py      clean and tokenize text
src/extract.py         skills, experience, education
src/match.py           hybrid match score
src/builder.py         JD-tailored resume draft
src/resume_format.py   HTML preview and PDF export
```

