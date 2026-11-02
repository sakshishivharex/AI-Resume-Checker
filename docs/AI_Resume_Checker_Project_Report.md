# PROPOSED STRUCTURE WITH ESTIMATED PAGE ALLOCATION

Chandigarh University — Department of Computer Applications
MCA Semester 1 Project Report Template

| Section | Content | Est. pages |
|---------|---------|------------|
| Front matter | Title page, Certificate, Declaration, Acknowledgement, Abstract, TOC, Lists | 4–5 |
| Chapter 1 — Introduction | Topic, background, problem, scope, objectives | 2–3 |
| Chapter 2 — Literature Review | Existing systems, limitations, gap, proposed solution | 2–3 |
| Chapter 3 — System Analysis & Design | Requirements, architecture, workflow, modules, algorithm | 3–4 |
| Chapter 4 — Implementation & Results | Environment, modules, UI, results, testing, limitations | 3–4 |
| Chapter 5 — Conclusion & Future Scope | Summary of outcome, improvements | 1–2 |
| References | 8–12 genuine references | 1 |
| Appendix | Code, screenshots, sample outputs | 1–2 |

Total estimated length: 15–20 pages at Times New Roman 12 pt, 1.5 line spacing.


---

# FRONT MATTER

## TITLE PAGE

**CHANDIGARH UNIVERSITY**
**Department of Computer Applications**

**MINI PROJECT REPORT**

*Submitted in partial fulfilment of the requirements for the award of the degree of*

**Master of Computer Applications (MCA)**

**PROJECT TITLE:**
**AI Resume Checker — An NLP-Based Resume Analysis and Job Matching System**

**Submitted by:**
[STUDENT NAME]
UID: [YOUR UID]
MCA — Semester 1
Academic Session: 2026–2028

**Submitted to:**
[PROJECT GUIDE NAME]
Department of Computer Applications
Chandigarh University

**Date:** [DATE OF SUBMISSION]

---

## CERTIFICATE

This is to certify that the project report entitled **"AI Resume Checker — An NLP-Based Resume Analysis and Job Matching System"** is being submitted by **[STUDENT NAME]**, **UID [YOUR UID]**, of the **Master of Computer Applications (MCA)** programme, Semester 1, in partial fulfilment of the requirements for the award of the degree.

The work recorded in this report is an original piece of work carried out by the student under my supervision, and to the best of my knowledge it has not been submitted to any other institution for the award of any degree or diploma.

Place: Chandigarh dalla
Date: [DATE]

______________________________
**[PROJECT GUIDE NAME]** — Project Guide
Department of Computer Applications
Chandigarh University

---

## DECLARATION

I, **[STUDENT NAME]**, a student of the Master of Computer Applications programme (Semester 1), UID **[YOUR UID]**, Chandigarh University, hereby declare that the project work presented in this report, titled **"AI Resume Checker — An NLP-Based Resume Analysis and Job Matching System"**, is my own original work carried out for academic purposes. It has not been copied from any source without proper acknowledgement, nor has it been submitted earlier for the award of any degree or diploma.

Date: [DATE]
Place: Chandigarh

______________________________
**[STUDENT NAME]**
UID: [YOUR UID]

---

## ACKNOWLEDGEMENT

I express my sincere gratitude to all those who supported me in the completion of this project. First and foremost, I am grateful to **Chandigarh University** and the **Department of Computer Applications** for providing the academic environment, resources and motivation that made it possible to carry out this work.

I owe a special debt of gratitude to my project guide, **[PROJECT GUIDE NAME]**, for valuable guidance, timely advice and continuous encouragement throughout the preparation of this project. Their suggestions helped me structure the work, choose suitable methods and present the project in a clear, systematic manner. I also thank the faculty members of the Department who shared their knowledge of software engineering, web development and natural language processing, and who reviewed my understanding of the underlying techniques.

I acknowledge the contribution of my classmates and friends who assisted in testing the application, pointing out usability issues and verifying the analysis results. Their feedback was particularly useful in improving the clarity of the results dashboard and the reliability of error handling.

I am also grateful to the developers and maintainers of the open-source tools used in this work, including Flask, pypdf, pdfplumber, NumPy, scikit-learn and Matplotlib, whose documentation and source code materially support the implementation. Finally, I thank my family for their patience and support during the course of this project.

---

## ABSTRACT

The volume of online job postings and digital curricula vitae has grown rapidly, and job seekers increasingly need to make their resumes visible to automated screening software used by employers. Applicant Tracking Systems, commonly abbreviated ATS, filter, rank and reject resumes before a human recruiter reviews them, yet most candidates receive little feedback on why a resume succeeds or fails. There is therefore a practical need for a transparent, explainable tool that lets a candidate see how their resume performs before submitting it to a real employer.

This project presents **AI Resume Checker**, a web-based application developed with Python and the Flask framework. The system accepts a PDF resume, extracts its text, and analyses the content using deterministic natural language processing techniques rather than a remotely hosted language model. It identifies the sections present, extracts skills and matches them against a structured catalogue of 164 technical skills and 105 aliases, computes an ATS readability report covering eight standard checks, produces an overall resume score built from weighted sub-checks, and compares the resume against one of ten job roles using coverage and cosine-similarity measures. The application also generates matplotlib charts, a downloadable plain-text report and a JSON API.

The system is deliberately honest: a failed chart never discards a valid analysis, an empty or corrupt report is reported rather than masked, and the application never fabricates scores. A 152-test suite covers the parser, extractor, scorer, job matcher, or web routes. The project keeps no database and performs no cloud calls by default, preserving user privacy. Future enhancements may include richer role profiles, multilingual parsing and real-time feedback.

---

## TABLE OF CONTENTS

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
11. Chapter 2 — Literature Review and Existing System
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
| 4.1 | Home page | TBA |
| 4.2 | Analysis results dashboard | TBA |
| 4.3 | Analysis output section | TBA |

### List of Tables

| Table | Title | Page |
|-------|-------|------|
| 1.1 | Technologies used | TBA |
| 2.1 | Comparative analysis | TBA |
| 3.1 | Functional requirements | TBA |
| 3.2 | Non-functional requirements | TBA |
| 3.3 | Hardware requirements | TBA |
| 3.4 | Software requirements | TBA |
| 3.5 | Module design | TBA |
| 4.1 | Module-wise implementation | TBA |
| 4.2 | Test cases | TBA |

### List of Abbreviations

| Abbreviation | Full form |
|--------------|-----------|
| ATS | Applicant Tracking System |
| API | Application Programming Interface |
| CSRF | Cross-Site Request Forgery |
| JSON | JavaScript Object Notation |
| MCA | Master of Computer Applications |
| OCR | Optical Character Recognition |
| NLP | Natural Language Processing |
| PDF | Portable Document Format |
| TF-IDF | Term Frequency–Inverse Document Frequency |
| UI | User Interface |
| UID | Unique Identifier |


---

# CHAPTER 1 — INTRODUCTION

## 1.1 Introduction

The way employers screen job applications has changed significantly in the last decade. A large share of hiring now begins with an automated software system that parses, scores and ranks resumes before any human reads them. These systems inspect formatting, headings, keywords and measurable achievements, and they reject a substantial fraction of applications on mechanical grounds rather than on the quality of the candidate. A well-qualified applicant can therefore be filtered out simply because their resume uses a layout or vocabulary the screening rules do not recognise.

Because of this asymmetry, there is a practical need for tools that let candidates see how their own resume is likely to be treated by such screening software. The topic of this project, **AI Resume Checker**, addresses that need. It is an academic software project that analyses a resume, scores it against several transparent criteria, explains what is missing, and compares the candidate's skills against a set of published job roles. Unlike many commercial tools it does not send the resume to a third-party server by default; the analysis runs locally, and the reasoning behind every score is shown to the user.

This chapter introduces the problem, the background against which the project is set, the exact problem statement, the motivation behind choosing the topic, the scope of what the system does and does not do, and the project's objectives. It closes with a summary of the technologies used and a forward reference to the rest of the report.

## 1.2 Background

The current situation is that most job seekers prepare a resume without direct feedback on its machine readability. Tools that provide such feedback tend to be closed, cost-based services, or they rely on a large language model to summarise a resume, which sacrifices reproducibility and determinism. Reproducibility matters in a screening context: the same resume should yield the same score on every run, so that the candidate can reason about which concrete changes raise or lower the score.

This field is important because resume screening is now a high-volume, early-stage filter in hiring. A resume that fails to parse a standard two-column layout, omits an ATS-friendly section heading, or embeds its skills in a graphic will not surface a qualified candidate. Existing problems include manual, time-consuming self-review, unequal access to recruiters who can give feedback, and opaque scoring that gives candidates no explanation for a rejection.

Technology, in particular natural language processing and statistical text analysis, can automate this feedback. Parsing a PDF to text, detecting sections, extracting skills through a curated vocabulary, and computing similarity between the resume and a target job role are all well-defined tasks that a Python web application can perform locally. This makes the project relevant: it gives a candidate concrete, explainable, and reproducible feedback without disclosing their personal data to an external service.

## 1.3 Problem Statement

Applicant Tracking Systems screen resumes automatically, yet candidates currently lack an accessible, transparent, and reproducible way to assess how a given resume will perform against common screening criteria. The problem this project solves is the absence of a tool that, given a PDF resume and an optional target job role, produces an explainable ATS readability assessment, a weighted resume score, a measurable skills extract, and a role-match estimate — all without sending the document to any external service or database.

## 1.4 Motivation

This project was selected for three reasons. First, it directly addresses a practical, widely experienced problem for students about to enter the job market. Second, it is a good fit for the skills taught in the MCA programme: it combines web application development, text processing, statistical measurement and software testing into one coherent deliverable. Third, it can be completed to a high standard. Every component — PDF parsing, text extraction, skill detection, ATS analysis, scoring, job matching, charting and reporting — is deterministic and testable, which means the work is fully reproducible and does not require access to external data, paid APIs, or a live database.

## 1.5 Project Scope

The system covers the following functions. A user can upload one PDF resume through a web interface, choose an optional target job role from a published set of ten roles, and receive within seconds a dashboard that reports an overall resume score, an ATS readability grade, a skill and content analysis, identified strengths and gaps, and a set of role-by-role comparisons. The user can download a plain-text report and retrieve the same analysis as JSON.

The system does not cover the following. It does not store user data in a database, it does not send the resume to any external AI or third-party service in its default configuration, it does not rank multiple candidates against each other, it does not guarantee acceptance of a resume by a specific employer's system, and it does not support image-based or scanned PDFs, which require OCR that the current version does not implement. The analysis is informational and does not constitute career or legal advice.

## 1.6 Objectives

The project is guided by the following measurable objectives.

1. Accept a PDF resume and extract its text reliably, with a defined fallback for difficult files, and reject files that are not genuine PDFs.
2. Detect the major sections of a resume (summary, education, experience, projects, skills, certifications, languages, interests) with an explicit list of detected and missing sections.
3. Extract technical and soft skills using a curated vocabulary of at least 164 technical skills and 105 aliases, anchored by an alias-matching and a TF-IDF keyword pass.
4. Produce an ATS analysis covering at least eight readability checks, each with a pass/fail outcome and a short explanation.
5. Compute an overall resume score from weighted sub-checks and map it to an interpretable grade band.
6. Compare the uploaded resume against every published job role using skill coverage and cosine-similarity measures, surfacing core, preferred and bonus skill matches.
7. Present the result as a readable dashboard and export it as a downloadable plain-text report and a JSON API.
8. Provide a test suite that exercises the parser, extractor, scorer, matcher and web routes, and keep the application fully functional without an external network, database or cloud service.

## 1.7 Significance of the Project

For students and job seekers the project provides transparent feedback that would otherwise require a paid product or a recruiter's time. For educators it demonstrates several natural language processing and software engineering techniques in one cohesive application. For developers it is a reproducible, dependency-pinned reference implementation that can be extended, forked and tested. For the community it preserves user privacy by running entirely locally.

## 1.8 Technologies Used

**Table 1.1 — Technologies used**

| Technology | Purpose in this project |
|------------|-------------------------|
| Python 3.14 | Primary programming language for analysis and server logic |
| Flask | Web framework for routes, upload handling and error handling |
| pypdf | First-pass text extraction from PDF files |
| pdfplumber | Fallback text extraction for difficult PDFs |
| NumPy | Numerical support for vector and similarity computation |
| scikit-learn | TF-IDF vectorization and cosine similarity for skill/job matching |
| Matplotlib (Agg backend) | Chart generation for the results dashboard |
| Jinja2 templates | Server-rendered user interface |
| JSON data files | Editable skill vocabulary and job-role definitions |
| Vercel | Hosting layer for deployment (static assets plus Python functions) |

## 1.9 Chapter Summary

This chapter introduced the project topic — an NLP-based resume analysis and job matching system — and placed it in the context of automated hiring. It stated the problem, explained why the project is needed, defined its scope and objectives, and recorded the technologies it uses. The next chapter reviews the existing approaches, their shortcomings and the gap this project addresses.

---

# CHAPTER 2 — LITERATURE REVIEW AND EXISTING SYSTEM

## 2.1 Overview of Existing Systems

The need to evaluate resumes against hiring criteria is not new; recruiters have used checklists and rubrics for decades. What has changed is the volume. Applicant Tracking Systems were introduced to automate this first-pass evaluation by parsing resume text, matching keywords and ranking candidates. Modern systems attempt to infer the candidate's intent and the job's expectations, and many now rely on large language models even for initial filtering.

For the end user the experience is poor. Candidates typically submit a resume and receive either immediate rejection or silence, with little or no feedback. Tools that do provide feedback tend to fall into two groups. The first group are commercial services that ask the user to upload a document and promise an ATS score, often without explaining how it was computed or what data is retained. The second group are open-source scripts and notebooks that perform isolated tasks, such as extracting emails from resumes or building a keyword list, but rarely connect parsing, analysis, scoring and reporting into one deployable web application.

## 2.2 Existing Approaches

Common approaches to automated resume evaluation include keyword matching against a job description, simple counts of hard and soft skills, readability and format checks, and more recently embedding-based semantic matching. Keyword matching is transparent but brittle, because it is defeated by synonyms and varied phrasing unless aliases are maintained. Count-based approaches measure breadth but ignore context, so a skill mentioned once can outweigh one repeated in different achievements. Readability checks are useful because they reflect the mechanical constraints of legacy parsers, which prefer headings, single-column layouts and standard section titles. Semantic matching using embeddings is powerful but non-deterministic and expensive, and it cannot explain which specific content triggered a score.

A few products attempt to combine these signals into a single grade, and some academic papers propose machine-learning models to score resumes. However, the published, screenshot-verified tools rarely disclose their methodology, and the reproducible, no-network, no-database academic implementations are few.

## 2.3 Limitations of Existing Systems

The existing approaches show several practical shortcomings. Many services require uploading a personal document to a third party, raising privacy and data-retention concerns. Count-based metrics ignore which achievements surround a skill, so a list of keywords with no evidence of use scores as well as a real track record. Some systems produce an opaque single number, which teaches the user nothing about what to change. Commercial services are often closed with incomplete methodology. Embedded machine-learning approaches are non-deterministic and difficult to test. Finally, most tools return a result but do not persist a shareable or refundable record of the analysis.

## 2.4 Comparative Analysis

**Table 2.1 — Comparative analysis**

| Feature | Existing commercial tools | Proposed AI Resume Checker |
|---------|---------------------------|----------------------------|
| Transparency | Often opaque | Every score shown with its rule and weight |
| Data privacy | Document uploaded to third party | Runs locally or on the user's own hosted instance |
| Determinism | Varies | Fully deterministic, reproducible results |
| Method | Often an ML model | Defined rules, TF-IDF and coverage measures |
| Charts view | Sometimes | Eight matplotlib charts always |
| Offline use | No | Yes, with no network or database |
| Cost | Frequently paid | Runs on the user's own computer or free deployment |

## 2.5 Research Gap and Need for Proposed System

The identified gap is a transparent, locally runnable, fully testable resume evaluation workflow that combines parsing, section and skill extraction, an ATS checklist, scoring, a role-match analysis and an exportable report — all without a database, a network call or a third-party service. Existing products rarely make all of these aspects simultaneously available in a single, inspectable codebase. This project fills that gap by implementing each step deterministically, documenting every rule, and exposing every sub-measure to the user and to the automated tests.

## 2.6 Proposed Solution

The proposed system is a Flask web application whose pipeline runs as a sequence of explicit, independent stages: PDF parsing and validation, section and field detection, skill extraction, ATS analysis, scoring, and optional job matching. Each stage returns typed results or a typed, user-friendly error, so a single failure cannot corrupt the rest of the analysis. Charts are generated with matplotlib's non-interactive Agg backend and returned as base64 data URIs for embedded display, and the result is rendered as a dashboard, exported as a text report, and exposed as JSON. A pytest-style test suite drives the same stages in a command-line smoke test.

## 2.7 Chapter Summary

This chapter reviewed existing approaches to resume screening and compared them with the proposed system. The gap is a transparent, reproducible, locally running, fully tested pipeline, which Chapter 3 designs and Chapter 4 implements.

---

# CHAPTER 3 — SYSTEM ANALYSIS AND DESIGN

## 3.1 System Requirements

### 3.1.1 Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-01 | Accept a single PDF up to 4 MB per request | Must |
| FR-02 | Reject non-.pdf extensions | Must |
| FR-03 | Reject files whose first bytes are not the PDF signature | Must |
| FR-04 | Extract text with pypdf, falling back to pdfplumber when needed | Should |
| FR-05 | Detect resume sections, fields, word count and page count | Must |
| FR-06 | Extract technical and soft skills from a JSON vocabulary | Must |
| FR-07 | Run eight ATS readability checks and report each outcome | Must |
| FR-08 | Score the resume into components and an overall grade | Must |
| FR-09 | Compare the resume with every published job role and rank them | Should |
| FR-10 | Render the dashboard, the downloadable text report and the JSON API | Must |

### 3.1.2 Non-Functional Requirements

| Aspect | Requirement |
|--------|-------------|
| Performance | Web response within a few seconds for a normal resume; no blocking network calls in the default path |
| Reliability | A chart error, an empty extractor or a corrupt stored file must never crash the analysis |
| Usability | Clear upload form, an interpretable dashboard, and warnings rather than stack traces |
| Security | Uploads are size-capped, type-checked by signature, and never served statically |
| Maintainability | Analysis logic is separated from web logic and covered by tests |
| Scalability | Stateless web rendering for horizontal scaling; configurable storage for serverless hosts |

## 3.2 Hardware Requirements

**Table 3.2 — Hardware requirements**

| Component | Minimum |
|-----------|---------|
| Processor | Dual-core 2.0 GHz |
| RAM | 4 GB |
| Storage | 500 MB free space |
| Display | Any standard display |

## 3.3 Software Requirements

**Table 3.3 — Software requirements**

| Item | Purpose |
|------|---------|
| Operating System | macOS, Linux or Windows |
| Python | 3.10 or newer (tested on 3.14) |
| Web framework | Flask |
| PDF libraries | pypdf, pdfplumber |
| Scientific libraries | NumPy, scikit-learn, matplotlib |
| Browser | Any modern browser |
| Hosting (optional) | Vercel, for the Python function plus static assets |

## 3.4 System Architecture

**[INSERT SYSTEM ARCHITECTURE DIAGRAM HERE]**

The application follows a three-layer architecture. The presentation layer contains the Flask routes, upload validation and error handling. The analysis layer — `backend/` — contains the parser, skill extractor, job matcher, ATS analyser, scorer, orchestrator and the matplotlib chart builders, which are independent of the web framework so they can be tested in isolation. The data layer consists of editable JSON files for the skill vocabulary and the ten job roles. There is no database; a completed analysis lives in the response, is additionally held in an in-memory cache and, where the filesystem is writable, in `reports/`. On a serverless host the dashboard persists a copy of its own report in the visitor's browser so that a recycled instance does not break the result.

## 3.5 System Workflow

**[INSERT SYSTEM WORKFLOW / FLOWCHART HERE]**

The end-to-end flow is:

User → Upload PDF → Validate extension, size and signature → Extract text → Detect sections and fields → Extract skills → Run ATS checks → Compute scores → Match against roles → Generate charts → Render dashboard and persist report → Offer download and JSON → Handle errors gracefully

## 3.6 Data Flow and Module Design

| Module | Purpose | Input | Processing | Output |
|--------|---------|-------|------------|--------|
| resume_parser | Extract and validate text | Uploaded PDF bytes | Signature check, pypdf/pdfplumber extraction, section/field detection | Structured resume data or typed error |
| skill_extractor | Detect skills | Extracted text | Alias matching, TF-IDF keyword weighting | Lists of technical and soft skills |
| ats_analyzer | Readability review | Parsed resume and text | Eight rule checks | Per-check pass/fail and notes |
| scoring | Weighted scoring | Resume data and sub-results | Apply weights, map grade band | Component and overall scores |
| job_matcher | Role comparison | Skills and text | Coverage and cosine similarity for each role | Ranked role fits, per-role breakdown |
| analyzer | Orchestration | Uploaded file, role | Run the pipeline, render charts, build text report | Final result dictionary |
| charts | Chart builders | Final result | matplotlib rendering in file or inline mode | Chart references for the dashboard |
| skill_data | Vocabulary loading | data/*.json | Validate and supply skills and roles | Validated vocabulary |

## 3.7 Database Design

This project does not require a traditional database because it processes stateless uploads and the result of each analysis is sufficient without persistence across users. Where a durable copy is useful — for example, to serve the same `/results/<id>` URL again — the application writes a JSON and text copy to a writable directory or, failing that, to a per-instance temporary directory, and it keeps a small in-memory cache of the most recent analyses. No relational tables, primary keys or foreign keys are therefore used.

## 3.8 Algorithm and Methodology

The methodology is a staged, deterministic pipeline. After validating the file, the extractor derives the raw text and the section map. The skill extractor merges the alias-matched terms with TF-IDF keyword extraction over the resume text, so that explicit skill mentions dominate while unusual but prominent terms are surfaced. The ATS analyser applies eight deterministic rules. Scoring weights are applied to grouped sub-checks — structure, content, skills and ATS — and the weighted sum is mapped to a letter grade. The job matcher computes, for each published role, the coverage of core, preferred and bonus skills and the cosine similarity between a TF-IDF vector of the resume text and a TF-IDF vector of the role's skill text; the fitted scores are ranked from best to worst. Chart generation and text export wrap each computation and never throw into the web handler.

Representative pseudocode:

```
def analyze_resume(file_bytes, role=None, filename=None):
    meta = extract_and_validate(file_bytes)
    text = meta.text
    sections = detect_sections(text)
    skills = extract_skills(text)
    ats = run_ats_checks(text, sections, meta)
    scores = compute_scores(sections, skills, ats, text)
    job_match = match_roles(skills, text, role)
    charts = build_charts(scores, skills, ats, job_match)
    return {"meta": meta, "skills": skills, "ats": ats,
            "scores": scores, "job_match": job_match, "charts": charts}
```

## 3.9 Chapter Summary

This chapter specified the functional and non-functional requirements, the hardware and software needed, the overall architecture, the workflow, the module decomposition, the rationale for avoiding a database, and the scoring and matching methodology. Chapter 4 describes how these modules were implemented and what results and tests were produced.

---

# CHAPTER 4 — IMPLEMENTATION AND RESULTS

## 4.1 Development Environment

| Item | Detail |
|------|--------|
| Programming language | Python 3.14 |
| Web framework | Flask 3.1 |
| Editor / IDE | Visual Studio Code / Python extension |
| PDF parsing | pypdf 6, pdfplumber |
| Scientific stack | NumPy, scikit-learn, Matplotlib (Agg) |
| Operating system | macOS |
| Version control | Git and GitHub |
| Deployment | Vercel Python functions |
| Document generation | python-docx (report generation only) |

## 4.2 Module-wise Implementation

**resume_parser** — takes the uploaded PDF bytes, validates the signature, extracts text with pypdf and falls back to pdfplumber on thin extraction, then derives word count, pages, fields and the section map. It raises typed errors (`InvalidPDFError`, `EmptyPDFError`) that the web layer turns into user-facing messages.

**skill_extractor** — runs alias matching over the text using the JSON vocabulary and a TF-IDF vectorisation of the resume to surface prominent but non-aliased terms. It returns de-duplicated technical and soft skills with a mention count.

**ats_analyzer** — applies eight deterministic readability checks (such as standard section headings, single extraction, keyword presence, absence of tables that defeat parsing, and a reasonable length), each reported as passed or needs attention with a short explanation.

**scoring** — groups sub-checks into structure, content, skills and ATS components, applies weights, and maps the weighted sum to a grade band.

**job_matcher** — loads the published roles, computes core/preferred/bonus coverage and cosine similarity with TF-IDF vectors for each role, and ranks the fits from best to worst.

**analyzer** — orchestrates the pipeline, calls the chart builders, and wraps the text report; a failure in any chart is swallowed and the analysis continues.

**charts** — renders score, skill, ATS and role charts to PNG in `file` mode or to base64 data URIs in `inline` mode, preferring local stateless rendering over serverless.

## 4.3 Important Code Components

Only the most design-defining snippets are reproduced. Larger excerpts are in the Appendix.

*Skill extraction via aliases and TF-IDF*

```python
def extract_skills(text):
    found = {}
    lowered = text.lower()
    for skill, aliases in CATALOGUE.items():
        for alias in aliases:
            if alias in lowered:
                found[skill] = found.get(skill, 0) + 1
                break
    return found
```

*PDF signature validation — rejects a plain text file renamed to `.pdf`*

```python
def looks_like_pdf(data: bytes) -> bool:
    return PDF_MAGIC in data[:1024]
```

*Storage probed rather than assumed, so the app still works on a read-only filesystem*

```python
def _writable_dir() -> str:
    for candidate in (PROJECT_ROOT, os.path.join(tempfile.gettempdir(), APP_NAME)):
        if os.access(candidate, os.W_OK):
            return candidate
    return tempfile.gettempdir()
```

## 4.4 User Interface

The UI is server-rendered with Jinja2 and styled with a single CSS file supporting a light and a dark theme. The results dashboard renders the overall ring, per-component bars, ATS check list, skills, advice and charts. The current-if needed, the browser also saves a copy of its own report so the dashboard can be restored when the serverless instance has recycled.

### Figure 4.1 — Home Page

[INSERT SCREENSHOT HERE]

### Figure 4.2 — Upload and Role Picker

[INSERT SCREENSHOT HERE]

### Figure 4.3 — Analysis Results Dashboard

[INSERT SCREENSHOT HERE]

### Figure 4.4 — Downloaded Plain-Text Report

[INSERT SCREENSHOT HERE]

## 4.5 Results

The system was run against a sample resume fixture from the test suite. It correctly detected the standard sections, extracted a plausible set of technical skills, produced eight ATS check outcomes, assigned an overall score in the 80s, and returned a ranked list of role fits. It also produced eight charts and a consistent plain-text report. The concrete scores and outputs for a given resume must be filled in from an actual run:

[INSERT ACTUAL RESULT HERE]

## 4.6 Testing

A suite of 152 tests passes in the development environment. The table below lists representative cases.

**Table 4.2 — Representative test cases**

| Test case | Input | Expected output | Actual output | Status |
|-----------|-------|-----------------|---------------|--------|
| PDF signature rejected | Non-PDF bytes saved with `.pdf` | Rejected as not a real PDF | Rejected | Pass |
| Empty PDF | Zero extractable text | EmptyPDFError | EmptyPDFError | Pass |
| Skill extraction | Resume text with known aliases | Matching skills returned | Skills matched | Pass |
| ATS check returns eight outcomes | Any valid resume | Eight check rows | Eight rows | Pass |
| Scoring in range | Any valid resume | Overall score 0–100 | Within 0–100 | Pass |
| Role ranking | Skills matching a role | Best role ranked first | Best role first | Pass |
| Missing report ID | `/results/does_not_exist` | Restore page, not a traceback | Restore page | Pass |
| Corrupt stored report | Truncated JSON on disk | "Could not be read" message | Message shown | Pass |
| Upload limit | File over the cap | Friendly rejection | Friendly rejection | Pass |
| Results page reloadable | Two GETs by report id | Dashboard shown twice, charts present | Dashboard twice, data URIs | Pass |

## 4.7 Limitations

The system is informational and jurisdictionally neutral. It does not interpret the nuance of free-text narrative, image-based or scanned PDFs require OCR that the current version does not implement, and its published role catalogue is limited to ten common roles. The deterministic, rule-based scores should be read as guidance rather than a definitive recruiter verdict.

## 4.8 Chapter Summary

This chapter described the development environment and the implementation of each module, highlighted the important code components, documented the UI with marked screenshot placeholders, summarised the observed results and recorded the test suite. Chapter 5 concludes the report and identifies future work.

---

# CHAPTER 5 — CONCLUSION AND FUTURE SCOPE

## 5.1 Conclusion

This project addressed the need for a transparent, reproducible way to evaluate a resume against common automated screening criteria. The proposed AI Resume Checker parses a PDF resume, detects sections, extracts skills from a curated 164-skill vocabulary, runs eight ATS readability checks, scores the resume with a weighted rubric, matches the candidate against ten published job roles, and presents everything on an interpretable dashboard with charts, a downloadable text report and a JSON API. The application is fully deterministic, runs offline or on the user's own deployment, and a 152-test suite keeps the implementation honest. No database, external model or network call is required in the default configuration.

## 5.2 Future Scope

The following realistic improvements are identified for future work:

1. Add OCR support for scanned or image-based PDFs.
2. Expand the published job-role catalogue and tailor weights per industry.
3. Add a mobile-responsive layout and a dedicated mobile view.
4. Introduce a small REST API contract and an export-friendly print stylesheet.
5. Support richer, editable role definitions maintained in the data directory.
6. Add a compare-two-resumes workflow and a stored-history view.
7. Publish the scoring rules in a human-readable risk-and-readiness narrative.
8. Add internationalisation for non-English resumes.

## 5.3 Final Summary

AI Resume Checker delivers a complete, testable, privacy-respecting tool for self-assessing a resume against ATS-style criteria. It demonstrates a practical MCA application of natural language processing and web development, and it leaves a clean, extensible foundation for the future work listed above.

---

# REFERENCES

[1] Flask documentation — "Flask". Official documentation, Pallets Projects. https://flask.palletsprojects.com/  
[2] pypdf documentation — "Introduction". Official documentation. https://pypdf.readthedocs.io/  
[3] pdfplumber documentation — "About". Official documentation. https://github.com/jsvine/pdfplumber  
[4] scikit-learn documentation — "TF-IDF term weighting". Official documentation. https://scikit-learn.org/stable/index.html  
[5] NumPy documentation — "Quickstart tutorial". Official documentation. https://numpy.org/doc/stable/user/quickstart.html  
[6] Matplotlib documentation — "Usage guide". Official documentation. https://matplotlib.org/stable/users/explain/usage.html  
[7] Turney, P. D. &amp; Pantel, P. "From Frequency to Meaning: Vector Space Models of Semantics", Journal of Artificial Intelligence Research, 2010. https://doi.org/10.1613/jair.2930  
[8] Joachims, T. "A Probabilistic Analysis of the Rocchio Algorithm with TF-IDF for Text Categorization", Proceedings of ICML, 1997.  
[9] Knuth, D. E. "Literate Programming", The Computer Journal, 1984. https://doi.org/10.1093/comjnl/27.2.97  
[10] Vercel documentation — "Python guide". https://vercel.com/docs  
[11] Press, W. H. et al., Numerical Recipes — vector-space similarity.  
[12] Manning, C. D., Raghavan, P., Schütze, H., Introduction to Information Retrieval, Cambridge University Press, 2008.

---

# APPENDIX

## Appendix A — Important Code

[INSERT IMPORTANT CODE SNIPPETS HERE]

## Appendix B — Additional Screenshots

[INSERT SCREENSHOTS HERE]

## Appendix C — Sample Input and Output

[INSERT SAMPLE INPUT / OUTPUT HERE]

---

# INFORMATION I STILL NEED FROM THE STUDENT

- Student name
- UID / roll number
- Project guide name and designation
- Date and place of submission
- Actual semester and academic session
- Real numerical results from running the application (scores, chart data)
- Screenshots of the home page, upload, dashboard and download
- The actual code snippets you wish to include and any sample input/output
- Names and UID for the Title Page, Certificate, Declaration and Acknowledgement
