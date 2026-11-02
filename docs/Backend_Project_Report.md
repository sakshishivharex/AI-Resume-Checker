# BACKEND PROJECT REPORT

## AI Resume Checker — Python / Flask Backend

**Department of Computer Applications, Chandigarh University**

Programme: Master of Computer Applications (MCA) — Semester 1
Academic Session: 2026–2028

---

## 1. Introduction

The backend of **AI Resume Checker** is a Python application built with the Flask web framework that turns an uploaded PDF resume into a scored, explained, role-aware analysis. It exposes HTTP routes for the web form and a JSON API, and it delegates all real work to an independent, framework-free analysis layer in the `backend/` package. Because the analysis layer has no web dependencies, every pipeline stage is unit-testable, and because the analysis is deterministic, the same resume produces the same result on every run. Nothing in the default path depends on a database, a remote model or a network call.

This report documents the backend: its structure, the responsibilities of each module, the storage and charting strategy that makes it safe on serverless hosts, its error-handling approach, and its test suite.

## 2. Backend Technology Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Web framework | Flask 3.1 | Routing, upload handling, validation, error pages |
| PDF intake | pypdf / pdfplumber | Text extraction, with a graceful fallback |
| Numeric / ML | NumPy, scikit-learn | TF-IDF vectors, cosine similarity, scoring support |
| Charts | Matplotlib (Agg) | Eight dashboard charts, file or inline mode |
| Config | Environment variables | `CHART_MODE`, `MAX_FILE_MB`, `STORAGE_DIR`, `SECRET_KEY` |
| Hosting | Vercel Python functions | Serverless deployment with static CDN |
| Tests | unittest | 152 automated tests over the pipeline and routes |

## 3. Backend Directory Layout

| Module | Responsibility |
|--------|----------------|
| `app.py` | Application factory, routes, upload validation, storage probing, report persistence, error pages |
| `backend/resume_parser.py` | PDF signature check, text extraction, section and field detection |
| `backend/skill_extractor.py` | Alias-based skill matching with a TF-IDF keyword pass |
| `backend/job_matcher.py` | Role coverage and cosine-similarity ranking over the catalogue |
| `backend/ats_analyzer.py` | Eight deterministic ATS readability checks |
| `backend/scoring.py` | Weighted component scores and the overall grade |
| `backend/analyzer.py` | Pipeline orchestration, advice narrative, plain-text report |
| `backend/charts.py` | Matplotlib chart builders, file/inline modes, cleanup, font-cache setup |
| `backend/skill_data.py` | Loading and validation of the JSON skill/role catalogue |
| `data/*.json` | Editable vocabulary of skills and job roles |

## 4. Request Lifecycle

1. The browser posts a PDF to `/analyze`.
2. `app.py` checks the extension, size (`MAX_FILE_MB`, defaults to 4), and the PDF file signature.
3. The pipeline runs: parse → sections/fields → skills → ATS checks → scores → role match → charts.
4. The result is persisted (disk where possible, memory and browser as a fallback) and the response redirects to `/results/<id>`.
5. `/results/<id>` renders the dashboard; `/report/<id>` downloads the text report; `/api/report/<id>` returns the JSON. A missing copy is recovered from the visitor's browser, not from the server.

## 5. Analysis Pipeline

PDF bytes in → structured sections, fields, skills, ATS outcomes, component scores, role ranking, charts and a plain-text report out. Each stage is wrapped so that an empty source or a single chart failure never discards the rest of the analysis. Typed exceptions (`InvalidPDFError`, `EmptyPDFError`, `UnknownRoleError`) are raised for invalid input and converted into friendly, non-technical messages at the web boundary.

## 6. Storage and Charting on a Read-Only / Stateless Host

`_writable_dir()` probes the project directory and falls back to the system temporary directory. `uploads/` and `reports/` derive from it. Matplotlib's font cache is pointed at a writable directory before import. Charts default to `inline` when the `VERCEL` variable is set, so nothing is written to a per-instance disk that another instance could not read. The most recent analyses are also held in an in-memory cache so a same-instance reload always works.

## 7. Error Handling and Privacy

Invalid PDFs, oversized uploads and empty files produce clear messages rather than stack traces. A corrupt stored report is reported as unreadable rather than being silently replaced. Uploaded PDFs are deleted after analysis unless `KEEP_UPLOADS=1` is set, and `uploads/` is never served statically. The application never calls an external AI or storage service by default.

## 8. Testing

| Area | Representative test | Result |
|------|--------------------|--------|
| Parser | Corrupt/non-PDF bytes rejected | Pass |
| Extraction | Section/section-skill extraction from a fixture PDF | Pass |
| ATS | All eight checks return an outcome per resume | Pass |
| Scoring | Overall score always within 0–100 | Pass |
| Job match | Ranking prefers the role that shares the most skills | Pass |
| Web routes | `/results/<id>` works after POST, reload and after restore | Pass |
| Storage | Missing without a file is detected; corrupt file reported as unreadable | Pass |
| Charts | Inline mode yields valid `data:` URIs and writes no PNG | Pass |

`152 tests pass.`

## 9. Conclusion

The backend is a clean separation of a deterministic analysis library from a thin Flask web layer. It is fully testable, runs without a database or network, and is engineered to remain functional on a serverless host by probing storage, inlining charts, and persisting a recoverable copy of each analysis in the visitor's own browser when no shared store is available.
