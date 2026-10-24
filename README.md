# Multimodal Construction Intelligence Platform

A Streamlit app for construction-site safety reviews, visual defect screening, project planning, and day-to-day site guidance. It uses Google Gemini for optional image analysis and chat, with built-in demo responses available when no API key is configured.

> **Safety notice:** This app provides AI-assisted screening and planning information only. It is not a substitute for an on-site inspection or the judgment of a licensed structural engineer or certified safety officer. Verify findings and applicable codes with qualified professionals.

## Features

- **Site Safety & PPE Audit** — Upload a JPG or PNG site photo to screen for visible PPE, count workers, identify potential hazards, and view suggested corrective actions. Reports can be downloaded as JSON.
- **Crack Diagnostics** — Upload a concrete or masonry photo to screen for visible defects, estimated crack width, severity, urgency, possible causes, and suggested follow-up. A scale reference in the photo can help provide context, but visual estimates are not measurements.
- **Planning & Valuation** — Explore indicative project budget, capex, asset value, milestone progress, and steel and cement requirements using editable-in-code planning assumptions for structure and location tiers.
- **Concept rendering** — Request an illustrative architectural image based on the selected project parameters and a customizable prompt.
- **Daily Site Assistant** — See weather-specific site advisories and ask construction questions. The live assistant can take the selected weather condition into account.
- **Demo mode** — The interface and report flow can be explored without a Gemini API key; AI analysis and chat then use built-in sample responses.

## Requirements

- Python 3.10 or newer
- A Google Gemini API key for live image analysis and conversational answers (optional)
- Internet access for Gemini features and the external concept-rendering service

## Run locally on Windows

Open PowerShell in the project folder and run:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install -r requirements.txt
python -m streamlit run app.py
```

Streamlit prints a local URL, usually `http://localhost:8501`, when the app starts.

## Configure Gemini (optional)

For a single session, paste a Gemini API key into the password-masked field in the sidebar. The app also reads `GEMINI_API_KEY` from Streamlit secrets.

To configure a local secret, create `.streamlit\secrets.toml`:

```toml
GEMINI_API_KEY = "your-api-key"
```

Keep API keys private. Do not commit `.streamlit\secrets.toml` or paste a key into source code. Without a key, the app runs in demo mode.

## Data and implementation notes

- Uploaded images are oriented, resized to a maximum side of 1600 pixels, and encoded as JPEG before live Gemini analysis.
- Analysis results are held in Streamlit session state; the app does not use a database.
- The planning and valuation figures are based on illustrative constants in `app.py`, not market quotes or certified estimates. Adjust them for local rates and obtain professional estimates before making decisions.
- Concept renders are illustrative, are requested from an external image service, and should not be treated as architectural or construction documents.
- The prompts reference OSHA 1926, IS 456:2000, and IS 13935 where relevant. References in generated output should be independently checked.

## Dependencies

See [`requirements.txt`](requirements.txt) for the Python dependencies.