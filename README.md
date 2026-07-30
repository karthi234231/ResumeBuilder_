# ResumeForge

> **Build, optimize, and export ATS-ready resumes in minutes — free, no login required.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-resumeforge--kj.netlify.app-4f46e5?style=for-the-badge&logo=netlify)](https://resumeforge-kj.netlify.app)
[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js)](https://nextjs.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

<a href="https://resumeforge-kj.netlify.app" target="_blank">
  <img src="https://api.microlink.io/?url=https%3A%2F%2Fresumeforge-kj.netlify.app&screenshot=true&meta=false&embed=screenshot.url" alt="ResumeForge Live Preview" width="100%" />
</a>

<p align="center">
  🔗 Live App &nbsp;→&nbsp; <a href="https://resumeforge-kj.netlify.app">https://resumeforge-kj.netlify.app</a>
</p>

---

## What is ResumeForge?

ResumeForge is a full-stack resume builder that combines a guided multi-step form, real-time live preview, LaTeX PDF generation, AI bullet enhancement, ATS scoring, and job description analysis — all in one place. Resume data lives entirely in your browser; no account, no cloud, no friction.

---

## Features

### Resume Builder
- **9-step guided wizard** — Personal Info → Summary → Experience → Education → Skills → Projects → Certifications → Achievements → Custom Sections
- **Live A4 preview** — updates as you type (150ms debounce), mirrors the PDF exactly
- **Accordion cards** — entries collapse to one-line summaries; active card expands
- **Drag-and-drop reordering** — bullets, entries, and section order all draggable
- **Undo / Redo** — 30-step history via `Ctrl+Z` / `Ctrl+Y`
- **Auto-save** — continuously persists to localStorage; session restores on page refresh
- **Ghost empty states** — every empty section shows faded example content to guide users
- **Dark / Light theme** — toggle stored in localStorage

### 12 Professional PDF Templates

All compiled with LaTeX for pixel-perfect typography.

| Template | Style |
|----------|-------|
| **Modern** | Clean two-tone with accent bar |
| **Classic** | Traditional chronological layout |
| **Minimal** | Ultra-clean, white-space focused |
| **Bold** | Strong headings, high contrast |
| **Elegant** | Refined serif typography |
| **Executive** | Senior professional, premium feel |
| **Academic** | Publication-ready academic CV |
| **Compact** | Tighter spacing for content-heavy resumes |
| **Sharp** | Geometric accents |
| **Stellar** | Modern gradient-touched |
| **Swiss** | Grid-based, design-influenced |
| **Tech** | Developer-optimized layout |

### Export Formats
| Format | Description |
|--------|-------------|
| **PDF** | LaTeX-compiled, print-ready, pixel-perfect |
| **DOCX** | Formatted Word document |
| **Plain Text** | ATS-safe, section-order aware |
| **JSON Backup** | Full resume state + template + styles — fully restorable |

### Resume Parsing — Upload & Auto-Fill
Upload any PDF or DOCX and every section auto-populates:
- Layout-aware extraction via PyMuPDF bounding boxes
- Font-size and bold detection for accurate section classification
- Multi-column layout detection (KMeans clustering)
- Date normalization to consistent `Mon YYYY` format
- Skill alias matching (`nodejs` → `Node.js`, `k8s` → `Kubernetes`)
- Fuzzy skill matching via `difflib` (0.88 cutoff)
- Gemini Vision fallback for scanned PDFs and complex layouts
- Per-field confidence score returned with every parse result
- Progressive animated fill — sections appear one by one as they are populated

### AI Bullet Enhancement
- Enterprise-grade rewrites with strong action verbs
- 7 domain profiles: Backend · Frontend · Data · DevOps · Leadership · Testing · General
- 3 angle alternatives per bullet: Impact · Leadership · Technical
- Async Gemini API call with local rule-based fallback

### ATS & Job Match Tools
| Tool | Description |
|------|-------------|
| **ATS Scorecard** | 0–100 score with category breakdown: contact, experience, skills, format, content |
| **Bullet Impact Scorer** | Each bullet scored 0–10 with actionable improvement tips |
| **Skills Gap Analyzer** | Role-specific readiness against 20+ job profiles |
| **JD Match Analyzer** | Paste any job description → instant keyword match % with present / missing / critical status |
| **Resume Health Report** | Error / Warning / OK per item with an A–F overall grade |
| **Passive Voice Detector** | Flags passive-voice bullets and suggests active replacements |
| **Buzzword Detector** | Catches overused terms like "synergy", "passionate", "team player" |
| **Readability Score** | Flesch-Kincaid score for professional readability |
| **Completeness Score** | 0–100 points-based checklist; click any item to jump to the relevant step |
| **Role Benchmark** | "Better than X% of Software Engineer resumes" comparison |

### Sharing
- Shareable read-only preview links (device-local, no server required)
- Anonymous mode — hides personal contact info before sharing
- Custom link labels and optional expiration

---

## Tech Stack

### Frontend
| Technology | Version | Purpose |
|-----------|---------|---------|
| Next.js | 14.2.3 | App framework (static export) |
| React | 18.3.1 | UI |
| TypeScript | 5.4.5 | Type safety |
| Tailwind CSS | 3.4.3 | Styling |
| Zustand | 4.5.2 | State management + localStorage persistence |
| dnd-kit | 6.1.0 | Drag-and-drop |
| Framer Motion | 11.2.9 | Animations |
| Lucide React | — | Icons |

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| FastAPI | 0.111.0 | REST API |
| PyMuPDF (fitz) | 1.24.3 | PDF text + layout extraction |
| python-docx | 1.1.2 | DOCX parsing and generation |
| Jinja2 | 3.1.4 | LaTeX template rendering |
| scikit-learn | 1.4.2 | TF-IDF JD matching + column detection |
| Pydantic | 2.7.1 | Data validation |
| google-genai | ≥1.5.0 | Gemini Vision (optional) |



## License

MIT — free to use, modify, and deploy.

---

*Built with Next.js · FastAPI · LaTeX · Gemini · Tailwind CSS*
