# MedGemma Navigator: DICOMweb + FHIR Demo

I participated in Kaggle’s **MedGemma Impact Challenge**, and my Kaggle notebook has **15+ upvotes** so far

This repo is a compact **Navigator-style** demo that links clinical context (FHIR) with imaging (DICOMweb) and runs **MedGemma** to generate a **single, reproducible run artifact** plus an optional **Gradio mini demo**.

---

## What's Inside
- 🖼️ **DICOMweb Integration**: Uses QIDO-RS to browse studies/series/instances and WADO-RS to fetch rendered image previews from public servers.
- 🧾 **FHIR R4 Context**: Pulls Patient details, Conditions, and Observations from public FHIR servers (with built-in failover for reliability).
- 🤖 **MedGemma Model**: Runs `google/medgemma-4b-it` (via Hugging Face Transformers) on the image + FHIR context to produce structured JSON outputs, like imaging summaries and pre-visit packets.
- 🧭 **Navigator Artifact**: Saves a single JSON file per run combining DICOM trace, FHIR data, and model outputs.
- 🧪 **Gradio Mini UI**: Optional interactive demo to run the pipeline and view results.

## What this demo does
1. Pulls a **DICOMweb rendered preview** (image) and records the DICOMweb **trace** (what was queried and retrieved).
2. Pulls **FHIR R4 context** (Patient + a few Conditions/Observations).  
3. Runs **MedGemma** using:
   - the image
   - the FHIR context snippet
   - a Navigator-style instruction prompt (structured output)
4. Saves outputs to `artifacts/` and optionally launches a Gradio UI.

## How to run (Kaggle)

1. Create a Kaggle Notebook and upload `medgemma-navigator-dicomweb-fhir.ipynb` (or paste the cells).
2. Turn **Internet ON**.
3. Add Hugging Face token (only if needed) as a Kaggle Secret:
   - `HF_TOKEN` = `...`
4. Run the notebook top-to-bottom.
5. If you run the Gradio cell, open the provided public link (Kaggle will show it in the output).


## Outputs
- **Artifact File**: `artifacts/full_run_<timestamp>.json` – Includes DICOM trace, FHIR context, raw MedGemma output, and parsed JSON.
- **Image Preview**: Optionally saved as `artifacts/dicom_preview_<timestamp>.png`.
- **Gradio UI**: Shows the image, context, outputs, and any errors for easy debugging.

## Notes
- Public servers might rate-limit; the demo handles failures gracefully.
- For offline use, point to a local model and skip network calls.
- Don't commit tokens—use secrets or env vars.
- FHIR and DICOM data aren't always linked in this demo; prompts avoid assuming connections to prevent misinformation.








