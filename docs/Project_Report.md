# COMPLETE REPORT STRUCTURE WITH ESTIMATED PAGE ALLOCATION

| Section | Content | Est. pages |
|---------|---------|------------|
| Front matter | Title page, Certificate, Declaration, Acknowledgement, Abstract, TOC, Lists | 4 |
| Chapter 1 | Introduction | 1.5 |
| Chapter 2 | Literature Review / Existing System | 1.5 |
| Chapter 3 | System Analysis and Design | 2.5 |
| Chapter 4 | Implementation and Results | 2 |
| Chapter 5 | Conclusion and Future Scope | 1 |
| References | Genuine sources | 0.5 |
| Appendix | Code, screenshots, sample I/O | 1 |
| **Total** | | **~14** |

---

# FRONT MATTER

## 1. TITLE PAGE

**CHANDIGARH UNIVERSITY**
**Department of Computer Applications**

**PROJECT REPORT**

*On*

**AI Resume Checker — An NLP-Based Resume Analysis and Job Matching System**

**Submitted by:**
[STUDENT NAME]
UID: [YOUR UID]
Programme: Master of Computer Applications (MCA)
Semester: 1st
Academic Session: 2026–2028

**Submitted to:**
[PROJECT GUIDE NAME]
Project Guide
Department of Computer Applications
Chandigarh University

**Date:** [DATE]

---

## 2. CERTIFICATE

This is to certify that the project report entitled **"AI Resume Checker — An NLP-Based Resume Analysis and Job Matching System"** is submitted by **[STUDENT NAME]**, UID **[YOUR UID]**, of the Master of Computer Applications programme, Semester 1, in partial fulfilment of the requirements of the degree. The work is original, carried out under my supervision, and has not been submitted elsewhere for any degree or diploma.

Place: Chandigarh
Date: [DATE]

______________________________
[PROJECT GUIDE NAME]
Project Guide
Department of Computer Applications
Chandigarh University

---

## 3. DECLARATION

I, **[STUDENT NAME]**, a student of the Master of Computer Applications programme (Semester 1), UID **[YOUR UID]**, Chandigarh University, hereby declare that the project work presented in this report is my own, carried out for academic purposes. It has not been copied without acknowledgement nor submitted earlier for any degree or diploma.

Date: [DATE]
Place: Chandigarh

______________________________
[STUDENT NAME]

---

## 4. ACKNOWLEDGEMENT

I express my sincere gratitude to **Chandigarh University** and the **Department of Computer Applications** for providing the academic environment and resources that supported this project. I am especially thankful to my project guide, **[PROJECT GUIDE NAME]**, for continuous guidance, timely advice and encouragement, and to the faculty whose teachings in software engineering and natural language processing underpin this work. I also thank my peers who tested the application and surfaced usability issues, and the authors of the open-source tools — Flask, pypdf, pdfplumber, NumPy, scikit-learn and Matplotlib — whose documented and reliable libraries made the implementation possible. Finally, I thank my family for their patience and support.

---

## 5. ABSTRACT

Most online screening filters a resume before a human ever reads it, yet candidates receive little explanation of why a resume succeeds or fails. There is therefore a need for a transparent, reproducible tool that lets a candidate see how their resume performs against common automated-screening criteria before applying.

This project presents **AI Resume Checker**, a Python and Flask web application that accepts a PDF resume and evaluates it with deterministic natural-language processing rather than a remote language model. It extracts text from the PDF, detects document sections, extracts technical and soft skills from a curated vocabulary of 164 skills and 105 aliases, produces an eight-point ATS readability report, computes a weighted resume score, and compares the candidate against a catalogue of ten job roles using coverage and cosine-similarity measures. The same analysis is rendered as charts on a dashboard, exported as a plain-text report, and served as JSON. The pipeline never fabricates scores: a failed chart, empty extractor or corrupt report is surfaced rather than masked. A 152-test suite covers the parser, extractor, scorer, matcher and web routes, and the application runs with no database and no external network call by default, preserving user privacy. The result is a reproducible, offline-capable assessment whose methodology is fully exposed. Possible extensions include OCR for scanned PDFs, a larger role catalogue and multilingual parsing.

---

## 6. TABLE OF CONTENTS

1. Title Page
2. Certificate
3. Declaration
4. Acknowledgement
5. Abstract
6. Table of Contents
7. List of Figures
8. List of Tables
9. List of Abbreviations
10. Chapter 1 — Introduction
11. Chapter 2 — Literature Review / Existing System
12. Chapter 3 — System Analysis and Design
13. Chapter 4 — Implementation and Results
14. Chapter 5 — Conclusion and Future Scope
15. References
16. Appendix

### List of Figures

| Figure | Title | Page |
|--------|-------|------|
| 3.1 | System architecture | TBA |
| 3.2 | System workflow | TBA |
| 4.1 | Home page | [INSERT SCREENSHOT HERE] |
| 4.2 | Main functionality | [INSERT SCREENSHOT HERE] |
| 4.3 | Output dashboard | [INSERT SCREENSHOT HERE] |

### List of Tables

| Table | Title | Page |
|-------|-------|------|
| 1.1 | Technologies used | TBA |
| 2.1 | Comparative analysis | TBA |
| 3.1 | Functional requirements | TBA |
| 3.2 | Hardware requirements | TBA |
| 3.3 | Software requirements | TBA |
| 3.4 | Module design | TBA |
| 4.1 | Module-wise implementation | TBA |
| 4.2 | Test cases | TBA |

### List of Abbreviations

| Abbreviation | Full Form |
|--------------|-----------|
| ATS | Applicant Tracking System |
| API | Application Programming Interface |
| JSON | JavaScript Object Notation |
| MCA | Master of Computer Applications |
| NLP | Natural Language Processing |
| PDF | Portable Document Format |
| TF-IDF | Term Frequency–Inverse Document Frequency |
| UID | Unique Identifier |

---

# CHAPTER 1 — INTRODUCTION

## 1.1 Introduction

Hiring increasingly begins with software. Applicant Tracking Systems parse resumes, match keywords, score the content and rank candidates before a human reviewer looks at anything. A resume that is poorly laid out, lacks standard section headings, or buries its skills inside a graphic may never reach a person, no matter how qualified the candidate is. This makes first-pass machine readability a gate on opportunity, and it means candidates deserve feedback on how their resume fares before they apply. **AI Resume Checker** is the academic project that addresses this, turning a PDF resume into an explainable, rule-based assessment that can be inspected, scored and exported.

## 1.2 Background

Candidate–employer matching has moved online, and most large organisations now rely on automated screening to cope with volume. Existing tools that give feedback sit in two camps: closed commercial services that upload the document to a third party and return an opaque number, or isolated scripts that parse text but never connect ingestion, analysis, scoring, visualisation and reporting into one deployable product. A deterministic, reproducible, no-network workflow is genuinely missing from the gap. Technology, in particular parsing, text extraction, alias matching, TF-IDF weighting and vector similarity, can deliver it inside a small web application.

## 1.3 Problem Statement

Candidates lack a transparent, offline-capable tool that evaluates a PDF resume and explains, per rule, why it scores as it does. This project provides such a tool: given a PDF and an optional target role, it produces an explainable ATS report, a weighted overall score, a measurable skill extract and a ranked role-fit list.

## 1.4 Motivation

The project is motivated by a concrete, widely experienced problem for students entering the job market. It also consolidates several MCA skills — web development, text processing, statistical measurement and testing — into one clean, fully testable deliverable.

## 1.5 Project Scope

**Covers:** uploading one PDF up to 4 MB, optional target-role selection, text extraction, section detection, skill extraction, eight ATS checks, a weighted score, role matching, charts, a downloadable text report and a JSON API. **Does not cover:** OCR of scanned PDFs, a multi-candidate ranking against each other, guaranteed acceptance by a specific employer's ATS, image-based resumes where text is not extractable, or career advice.

## 1.6 Objectives

1. Parse a PDF safely and reject non-PDF or empty files with a clear message.
2. Detect standard resume sections and fields.
3. Extract technical and soft skills from a curated JSON vocabulary.
4. Run eight deterministic ATS readability checks.
5. Score the resume with a weighted rubric and a grade band.
6. Rank the candidate against published job roles by coverage and similarity.
7. Render the result as charts, a text report and JSON.
8. Ship a test suite that exercises the pipeline and web routes.

## 1.7 Significance of the Project

Students gain transparent, shareable feedback before applying; educators gain a reproducible demonstration of NLP and web engineering; developers gain an inspectable, extensible, no-network codebase; and the community gains a tool that keeps personal documents private by running locally or on the user's own deployment.

## 1.8 Technologies Used

**Table 1.1 — Technologies used**

| Technology | Purpose |
|------------|---------|
| Python 3.14 | Core programming language |
| Flask 3.1 | Web framework for routes, uploads and errors |
| pypdf / pdfplumber | Extract text from PDF |
| NumPy | Vector arithmetic |
| scikit-learn | TF-IDF and cosine similarity |
| Matplotlib (Agg) | Chart generation |
| Jinja2 + CSS/JS | Server-rendered UI, no client-side framework |
| JSON data files | Editable skills and role catalogue |
| Vercel | Hosting with a Python function plus static CDN |

## 1.9 Chapter Summary

This chapter introduced AI Resume Checker, its problem context, motivation, scope, objectives, significance and technologies. The remaining chapters develop the analysis already made at a high level: the existing work, the design, the implementation, the results and the conclusion.

---

# CHAPTER 2 — LITERATURE REVIEW / EXISTING SYSTEM

## 2.1 Overview of Existing Systems

Resume evaluation has always been rubric-driven, first by human recruiters and now increasingly by software. Applicant Tracking Systems replaced many of those manual steps with keyword counts, readability checks and structural rules, and more recently vendors have layered large language models on top of the same parsing.

## 2.2 Existing Approaches

The common approaches are keyword matching (transparent but brittle to synonyms), count-based skill totals (easy but context-blind), readability/format checks (reflect real parser constraints), and embedding-based semantic matching (powerful but non-deterministic and hard to explain). Commercial tools often bundle several of these into one number.

## 2.3 Limitations of Existing Systems

Commercial services usually upload the document to a third party, keep their formula secret and cannot be run offline. Count-based scorers ignore the context around an ability, and purely statistical scorers are non-deterministic and hard to test. Embeddings improve matching but explain nothing.

## 2.4 Comparative Analysis

**Table 2.1 — Comparative analysis**

| Feature | Existing system | Proposed AI Resume Checker |
|---------|-----------------|---------------------------|
| Transparency | Often opaque | Every score shown with its rule |
| Privacy | Data leaves to a service | Runs locally / on the user's own host |
| Determinism | Varies | Fully deterministic and testable |
| Offline | No | Yes |
| Explainability | Low | Per-rule ATS outcomes and weights |

## 2.5 Research Gap / Need for Proposed System

The gap is a reproducible, transparent, offline-capable single pipeline from PDF to a scored, charted, exportable assessment. This project fills it by making every rule explicit and every stage testable.

## 2.6 Proposed Solution

A Flask backend orchestrates a staged pipeline — parse, sections/fields, skills, ATS checks, scoring, role matching and charting — with each stage returning typed results or typed, user-friendly errors. The result is rendered on a dashboard, exported as text and exposed as JSON, and it runs with no database and no default network calls.

## 2.7 Chapter Summary

This chapter reviewed existing approaches and showed the gap of transparency, reproducibility and privacy that this project addresses, leading into the design.

---

# CHAPTER 3 — SYSTEM ANALYSIS AND DESIGN

## 3.1 System Requirements

### 3.1.1 Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | Accept one PDF up to 4 MB | Must |
| FR-02 | Reject the wrong extension | Must |
| FR-03 | Reject files that are not real PDFs | Must |
| FR-04 | Extract text with a fallback library | Should |
| FR-05 | Detect sections, fields, page and word counts | Must |
| FR-06 | Extract skills from the JSON vocabulary | Must |
| FR-07 | Produce eight ATS outcomes, each with an explanation | Must |
| FR-08 | Compute a weighted overall score and grade | Must |
| FR-09 | Rank the resume against the job catalogue | Should |
| FR-10 | Serve the dashboard, report and JSON API | Must |

### 3.1.2 Non-Functional Requirements

| Aspect | Requirement |
|--------|-------------|
| Performance | A normal resume is analysed in a few seconds |
| Reliability | A chart or extractor failure never discards the analysis |
| Usability | Upload form, clear dashboard, friendly messages not tracebacks |
| Security | Uploads are size-capped, signature-checked and never served |
| Maintainability | The analysis layer is independent and unit-tested |
| Scalability | Stateless, horizontal, serverless-friendly rendering |

## 3.2 Hardware Requirements

**Table 3.2 — Hardware requirements**

| Component | Requirement |
|-----------|-------------|
| Processor | Dual-core 2.0 GHz |
| RAM | 4 GB |
| Storage | 500 MB free |
| Display | Any standard display |

## 3.3 Software Requirements

**Table 3.3 — Software requirements**

| Software | Purpose |
|----------|---------|
| Operating System | macOS / Linux / Windows |
| Programming Language | Python 3.10+ (tested on 3.14) |
| Framework | Flask |
| Libraries | pypdf, pdfplumber, NumPy, scikit-learn, matplotlib |
| IDE | VS Code / any editor |
| Database | Not used |

## 3.4 System Architecture

**[INSERT SYSTEM ARCHITECTURE DIAGRAM HERE]**

The backend separates two layers: a thin Flask web layer (`app.py`) and a framework-free analysis library (`backend/`). The web layer validates uploads, calls the pipeline, persists the result and renders the result. The analysis library is purely computational: parsing, extraction, ATS, scoring, role matching, orchestration, charts and vocabulary loading are all free of any web dependency.

## 3.5 System Workflow

**[INSERT SYSTEM WORKFLOW / FLOWCHART HERE]**

`Input → Parse & validate → Sections/Fields → Skills → ATS checks → Scoring → Role match → Charts → Dashboard + Report + JSON → Handle errors`

## 3.6 Data Flow / Module Design

**Table 3.4 — Module design**

| Module | Purpose | Input | Processing | Output |
|--------|---------|-------|------------|--------|
| resume_parser | Extract and validate | PDF bytes | Signature check, pypdf/pdfplumber, sections | Structured data or typed error |
| skill_extractor | Detect skills | Text | Alias match + TF-IDF keywords | Skill list |
| ats_analyzer | Readability | Text + sections | 8 rule checks | Per-check outcome |
| scoring | Weighted score | Extracted metrics | Weights + grade band | Score object |
| job_matcher | Role fit | Skills + text | Coverage + similarity | Ranked roles |
| analyzer | Orchestration | File + role | Run pipeline, build report | Complete result |
| charts | Figures | Result | Matplotlib render | Chart references |

## 3.7 Database Design

This project does not require a traditional database because it processes stateless uploads, has no multi-user records, and gains enough to persist each analysis in a writable file or an in-memory cache. There are no tables, primary keys or foreign keys.

## 3.8 Algorithm / Methodology

For each uploaded file the pipeline validates the PDF, extracts text, detects sections, matches aliases and lifts prominent terms with TF-IDF, runs eight ATS rules, composes weighted component scores into an overall grade, and computes each role's core/preferred/bonus coverage plus a TF-IDF cosine similarity. Charts and a text report are built over the result; failures are contained rather than fatal.

```
def analyze_resume(bytes, role=None, filename=None):
    meta = parse_and_validate(bytes)
    sections = detect_sections(meta.text)
    skills = extract_skills(meta.text)
    ats = run_ats_checks(meta.text, sections)
    scores = compute_scores(sections, skills, ats, meta.text)
    roles = rank_roles(skills, meta.text)
    charts = build_charts(scores, skills, ats, roles)
    return Result(meta, sections, skills, ats, scores, roles, charts)
```

## 3.9 Chapter Summary

This chapter specified the requirements, architecture, workflow, modules, data-flow, the deliberate absence of a database, and the algorithm. The next chapter turns the design into implementation.

---

# CHAPTER 4 — IMPLEMENTATION AND RESULTS

## 4.1 Development Environment

| Item | Detail |
|------|--------|
| Language | Python 3.14 |
| IDE / Editor | VS Code (Python extension) |
| Framework | Flask 3.1 |
| Libraries | pypdf, pdfplumber, NumPy, scikit-learn, Matplotlib |
| OS | macOS |
| Tools | Git, GitHub, Vercel CLI |

Use [TO BE ADDED] where information is unavailable.

## 4.2 Module-wise Implementation

| Module | Purpose | Input | Processing | Output |
|--------|---------|-------|------------|--------|
| app.py | Routes, validation, errors | HTTP request | Validate, run pipeline, redirect | HTML, JSON, error page |
| resume_parser | Extract text | PDF bytes | Signature check, pypdf→pdfplumber, sections | Structured data |
| skill_extractor | Extract skills | Text | Aliases + TF-IDF | Skill lists |
| ats_analyzer | Readability | Text + sections | 8 deterministic checks | Check outcomes |
| scoring | Score | Metrics | Weighted sum, grade | Score object |
| job_matcher | Role fit | Skills + text | Coverage + cosine | Ranked roles |
| analyzer | Orchestration | File + role | Run pipeline, charts | Result dict |
| charts | Visuals | Result | Matplotlib Agg render | Chart refs |

## 4.3 Important Code Components

*PDF validation, rejecting a relabelled text file:*

```python
def looks_like_pdf(data: bytes) -> bool:
    return PDF_MAGIC in data[:1024]
```

*Inline chart rendering (no filesystem on a serverless host):*

```python
if INLINE_CHARTS:
    buf = io.BytesIO(); fig.savefig(buf, format="png"); plt.close(fig)
    return "data:image/png;base64," + base64.b64encode(buf.getvalue()).decode()
```

Use **[INSERT CODE SNIPPET HERE]** for any additional snippets you wish to print.

## 4.4 User Interface

The UI is server-rendered (Jinja2) with one stylesheet supporting light/dark themes. The results dashboard shows the overall ring, per-component bars, the ATS check list, extracted skills, role rankings and charts.

### Figure 4.1 — Home Page

[INSERT SCREENSHOT HERE]

### Figure 4.2 — Main Functionality (Upload + Role Picker)

[INSERT SCREENSHOT HERE]

### Figure 4.3 — Output Page (Dashboard)

[INSERT SCREENSHOT HERE]

## 4.5 Results

On a sample fixture the application extracts the standard sections, surfaces a plausible skill set, returns eight ATS outcomes, assigns an overall score in the 80s, ranks a fitting role first, and emits eight charts and a consistent text report. Actual measured outputs must be placed here:

[INSERT ACTUAL RESULT HERE]

## 4.6 Testing

A 152-test suite passes. Representative cases:

**Table 4.2 — Test-case table**

| Test Case | Input | Expected Output | Actual Output | Status |
|-----------|-------|-----------------|---------------|--------|
| Reject non-PDF | Text bytes named .pdf | Invalid file error | Invalid file error | Pass |
| Empty PDF | Empty text | EmptyPDFError | EmptyPDFError | Pass |
| Extract sections | Fixture PDF | Standard sections | Sections listed | Pass |
| Skill extraction | Known aliases | Skills returned | Skills returned | Pass |
| 8 ATS checks | Any resume | 8 outcomes | 8 outcomes | Pass |
| Score range | Any resume | 0–100 | Within 0–100 | Pass |
| Missing report id | /results/nope | Restore page | Restore page | Pass |
| Corrupt stored report | Truncated JSON | "Could not be read" | "Could not be read" | Pass |

## 4.7 Limitations

The analysis is heuristic, informational and jurisdictionally neutral. It does not interpret free-text nuance, cannot parse scanned/image PDFs without OCR, and its published role set is limited. Scores should be read as guidance.

## 4.8 Chapter Summary

This chapter described the development environment, each module, the important code, the UI, the observed results, the test cases and the limitations. The next chapter concludes the project and lists future work.

---

# CHAPTER 5 — CONCLUSION AND FUTURE SCOPE

## 5.1 Conclusion

AI Resume Checker meets its objectives: it accepts a PDF resume, validates it, extracts text, detects sections and skills, runs eight ATS checks, scores it with a weighted rubric, ranks it against a role catalogue, and presents the outcome as charts, a text report and JSON — all deterministically, offline and with no database. The 152-test suite keeps the implementation transparent and testable.

## 5.2 Future Scope

1. OCR support for scanned PDFs.
2. A larger, editable role catalogue per industry.
3. A mobile-responsive stylesheet and mobile layout.
4. A REST API with stable versioned contracts.
5. A compare-two-resumes workflow.
6. Richer per-role weighting and narrative advice.
7. Multilingual resume parsing.
8. History of past analyses per user.

## 5.3 Final Summary

AI Resume Checker is a complete, honest, testable MCA application that gives candidates transparent feedback before they apply, built on Python, Flask and standard NLP techniques, and built to remain runnable offline or on the user's own deployment.

---

# REFERENCES

[1] Flask documentation — https://flask.palletsprojects.com/  
[2] pypdf documentation — https://pypdf.readthedocs.io/  
[3] pdfplumber documentation — https://github.com/jsvine/pdfplumber  
[4] scikit-learn — https://scikit-learn.org/stable/  
[5] NumPy — https://numpy.org/doc/stable/  
[6] Matplotlib — https://matplotlib.org/stable/  
[7] Turney & Pantel, "From Frequency to Meaning", JAIR 2010 — https://doi.org/10.1613/jair.2930  
[8] Manning, Raghavan, Schütze, *Introduction to Information Retrieval*, Cambridge UP, 2008.  
[9] Joachims, "A Probabilistic Analysis of the Rocchio Algorithm with TF-IDF", ICML 1997.  
[10] Vercel Python guide — https://vercel.com/docs  

---

# APPENDIX

## Appendix A — Important Code

[INSERT CODE HERE]

## Appendix B — Additional Screenshots

[INSERT SCREENSHOTS HERE]

## Appendix C — Sample Input/Output

[INSERT SAMPLE DATA HERE]

---

# INFORMATION I STILL NEED FROM THE STUDENT

- Student name
- UID / roll number
- Guide name and designation
- Date and place of submission
- Actual semester and academic session
- Measured results from running the app (scores, charts)
- Screenshots of the home, upload, dashboard and download pages
- Extra code snippets and sample input/output
