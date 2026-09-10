# MatGuide AI

An AI assistant that explains any construction material in a
structured format: Introduction, Composition, Properties, Purpose/
Use, Types/Grades, Standard Specs/Codes, Site Precautions, and
Alternatives — powered by the Groq API.

## Problem it solves

Site engineers, students, and contractors often don't have a fast,
reliable way to look up what a material actually is, its correct use,
grades, and precautions — leading to wrong material selection and
avoidable site delays.

## Stack (4 platforms)

| Platform | Role |
|---|---|
| Claude / ChatGPT | Used to write and debug the code during development |
| Streamlit | The app itself — UI + hosting via Streamlit Community Cloud |
| Groq API | Generates the structured material explanation |
| GitHub | Stores the code, connects to Streamlit Cloud for deployment |

## Project structure

```
matguide-ai/
├── app.py
├── requirements.txt
├── README.md
├── .gitignore
└── .streamlit/
    └── secrets.toml.example
```

## Run locally

```bash
pip install -r requirements.txt
cp .streamlit/secrets.toml.example .streamlit/secrets.toml
# edit .streamlit/secrets.toml and paste your real GROQ_API_KEY
streamlit run app.py
```

Get a free Groq API key at https://console.groq.com/keys.

(No key yet? You can also paste one directly into the sidebar in the
running app — it stays in memory for that session only, never saved
or committed.)

## Deploy to GitHub + Streamlit Community Cloud

```bash
git init
git add .
git commit -m "Initial MatGuide AI app"
git branch -M main
git remote add origin YOUR_GITHUB_REPOSITORY
git push -u origin main
```

Then:

```
GitHub Repository
      ↓
Streamlit Community Cloud → "New app"
      ↓
Select your repository + branch, main file: app.py
      ↓
App settings → Secrets → paste:
      GROQ_API_KEY = "gsk_..."
      ↓
Deploy
```

Never commit your real API key. `secrets.toml` is excluded via
`.gitignore` — only `secrets.toml.example` (with a placeholder) goes
to GitHub.

## Notes

- Answers are AI-generated from general engineering knowledge —
  always verify specific grades, strengths, and codes against your
  local specification/BOQ before relying on them for actual
  construction decisions.
- No database or RAG in this version — it's intentionally simple to
  build and deploy fast. A future version could ground answers in
  your own approved-materials list or local code documents (PDF/CSV)
  using the same retrieval approach as the Construction Progress
  Intelligence app, if you want more reliable, source-cited answers.
