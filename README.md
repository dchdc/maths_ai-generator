# Singapore Maths AI Question Generator

A Streamlit starter app for teachers creating Singapore Primary and Secondary maths quizzes from worksheets or pasted text. It uses Google Gemini (`gemini-3.6-flash` by default), lets teachers review/edit generated questions, saves quizzes in a local SQLite database, and provides a student quiz page with automatic marking and worked solutions.

## Requirements
- Python 3.10 or newer
- A Google Gemini API key enabled for the Google AI Studio project
- Internet access while generating questions

## Windows setup
1. Extract this ZIP into a folder, for example `C:\Users\Lenovo\Downloads\singapore_maths_ai_generator`.
2. Open Command Prompt in that folder.
3. Install dependencies:
   ```bat
   python -m pip install -r requirements.txt
   ```
4. Set your API key as a Windows user environment variable named `GEMINI_API_KEY`. Do not put the key into `app.py` or share it. Close and reopen Command Prompt after setting it.
5. Run:
   ```bat
   python -m streamlit run app.py
   ```
6. Open the local URL Streamlit prints, normally `http://localhost:8501`.

Optional: set `GEMINI_MODEL` to a model available to your API key. Default is `gemini-3.6-flash`.

## Workflow
1. Select the student level, topic(s), difficulty, question count, and answer mode.
2. Upload a PDF, DOCX, PNG, JPG, or TXT worksheet, or paste source text.
3. Generate draft questions. Review and edit every question, answer, and solution.
4. Publish to save a quiz in `quizzes.db` and get a link with a quiz ID.
5. Students open the quiz link, submit answers, and see their score and worked solutions.

## Important limitations
- Treat AI-generated answers and solutions as drafts. A teacher should verify all content before publishing.
- Scanned PDFs with little selectable text currently use only the first page as a visual fallback. For multi-page scans, export pages as images and process them separately or OCR them first.
- Typed marking checks exact text or equivalent numeric/simple symbolic expressions; it does not award method marks or understand a full marking rubric.
- The link created on localhost is only for your own computer. To share with students remotely, deploy the app to a hosting service and use the hosted base URL with the same `?quiz=ID` suffix. Ensure the database persists on the host.
- This is a starter application, not a hardened production service. Add authentication, access controls, rate limits, backups, and privacy safeguards before public deployment. Do not upload student personal data.

## Troubleshooting
- `GEMINI_API_KEY is not set`: add the environment variable and reopen Command Prompt.
- `503` / `504` model errors: wait briefly and retry; these may be temporary capacity or timeout errors.
- Model not found: choose a model listed as available to your API key by setting `GEMINI_MODEL`.


### Printable PDF worksheets
After generating and reviewing questions, use **Download questions as PDF** to export a printable worksheet. You can optionally include the answer key and worked solutions. Diagram-based questions are requested by default where suitable; diagrams are rendered as simple schematic figures in the PDF. Always check diagrams and AI-generated answers before distributing.
