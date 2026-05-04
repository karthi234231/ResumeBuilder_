# ResumeForge

> **Build, optimize, and export ATS-ready resumes in minutes — free, no login required.**

[![Live Demo](https://img.shields.io/badge/Live%20Demo-resumeforge--kj.netlify.app-4f46e5?style=for-the-badge&logo=netlify)](https://resumeforge-kj.netlify.app)
[![Next.js](https://img.shields.io/badge/Next.js-14-black?style=for-the-badge&logo=next.js)](https://nextjs.org)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.111-009688?style=for-the-badge&logo=fastapi)](https://fastapi.tiangolo.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)

---

<!-- Live site preview (auto-generated screenshot) -->
[![ResumeForge Preview](https://image.thum.io/get/width/1200/crop/675/https://resumeforge-kj.netlify.app/)](https://resumeforge-kj.netlify.app)

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

---

## API Endpoints

| Method | Path | Description |
|--------|------|-------------|
| `POST` | `/api/parse-resume` | Upload PDF/DOCX → structured JSON with confidence scores |
| `POST` | `/api/generate-pdf` | Resume JSON + template → LaTeX-compiled PDF |
| `POST` | `/api/export/docx` | Resume JSON → formatted DOCX |
| `POST` | `/api/enhance-bullet` | Single bullet → AI-enhanced version |
| `POST` | `/api/enhance-bullet/alternatives` | Single bullet → 3 angle variants |
| `POST` | `/api/enhance-bullets` | Batch bullet enhancement |
| `POST` | `/api/match-jd` | Resume + JD → TF-IDF cosine similarity score |
| `POST` | `/api/match-jd/quick` | Resume + JD → fast keyword count score |
| `GET`  | `/health` | Health check |

---

## Project Structure

```
ResumeBuilder/
├── frontend/
│   ├── app/
│   │   ├── builder/          # Main resume builder (side-by-side layout)
│   │   ├── r/[slug]/         # Shareable resume viewer
│   │   └── page.tsx          # Landing / welcome screen
│   ├── components/
│   │   ├── steps/            # 9 form step components
│   │   ├── templates/        # HTML/CSS live preview templates
│   │   ├── ATSScorecard.tsx
│   │   ├── JDAnalysisPanel.tsx
│   │   ├── ResumeHealthPanel.tsx
│   │   ├── PlainTextExportPanel.tsx
│   │   └── ShareableResumePanel.tsx
│   ├── store/
│   │   └── resumeStore.ts    # Zustand store (all state + persistence)
│   ├── lib/
│   │   ├── ats/              # ATS engine, keyword DB, bullet scorer, readability
│   │   ├── bulletEnhancer.ts
│   │   ├── jdAnalysis.ts
│   │   └── resumeHealth.ts
│   └── types/resume.ts       # TypeScript interfaces
│
└── backend/
    ├── main.py               # FastAPI app + CORS
    ├── routes/               # API route handlers
    ├── services/
    │   ├── parse_service.py  # Resume parser (PyMuPDF + Gemini fallback)
    │   ├── template_service.py
    │   └── latex_service.py  # LaTeX compilation pipeline
    ├── models/resume.py      # Pydantic models
    └── templates/            # 12 LaTeX .tex.jinja2 templates
```

---

## Local Development

### Prerequisites
- Node.js 20+
- Python 3.10+
- LaTeX distribution with `xelatex` and `pdflatex` on PATH:
  - Linux/macOS: [TeX Live](https://tug.org/texlive/)
  - Windows: [MiKTeX](https://miktex.org/)

### Frontend

```bash
cd frontend
npm install --legacy-peer-deps
npm run dev
# → http://localhost:3000
```

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt

# Optional: improved name/location recognition via spaCy NER
python -m spacy download en_core_web_sm

cp .env.example .env
# Add GEMINI_API_KEY to .env (optional — free at https://aistudio.google.com)

uvicorn main:app --reload --port 8000
# → http://localhost:8000
```

### Environment Variables

**`backend/.env`**
```env
# Optional — enables Gemini Vision for scanned PDF parsing and AI bullet enhancement
GEMINI_API_KEY=your_key_here
```

**`frontend/.env.local`**
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
```

---

## Deployment

### Frontend — Netlify

The `frontend/netlify.toml` handles the full build config:
- Build command: `npm run build` (static export → `out/`)
- Redirect: `/* → /index.html` (SPA catch-all for shareable links)
- Node 20, `--legacy-peer-deps`

Push to `main` → Netlify auto-deploys.

### Backend — Render / Railway / Fly.io

Requires a server environment with LaTeX installed.

1. Build: `pip install -r requirements.txt`
2. Start: `uvicorn main:app --host 0.0.0.0 --port $PORT`
3. Set `GEMINI_API_KEY` as an environment variable
4. Ensure `xelatex` is available in the build image (see `Dockerfile.worker`)

Then set `NEXT_PUBLIC_API_URL` in Netlify environment variables to your deployed backend URL.

---

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl/Cmd + Z` | Undo |
| `Ctrl/Cmd + Y` | Redo |
| `Escape` | Close any open modal, drawer, or dropdown |

---

## Accessibility

- Full ARIA labelling — `tablist/tab/tabpanel`, `progressbar`, `alert/status`, `dialog`, `combobox`
- Focus trap in modals; focus moves to first interactive element on open
- All animations respect `prefers-reduced-motion`
- Offline detection badge — download buttons disabled when browser has no internet

---

## Data Privacy

- **No account required** — zero sign-up, zero friction
- **All resume data stays in your browser** — localStorage only; nothing is sent to any server unless you click Download or use an AI feature
- **Shareable links** — stored in the browser of the device that created them; no cloud storage
- **Gemini API** — only called when `GEMINI_API_KEY` is configured; text is processed under Google's API privacy policy

---

## Roadmap

- [ ] Cover letter generator
- [ ] Interview preparation module
- [ ] Dashboard with multi-resume management
- [ ] Mobile-first responsive redesign
- [ ] Version history with named snapshots

---

## License

MIT — free to use, modify, and deploy.

---

*Built with Next.js · FastAPI · LaTeX · Gemini · Tailwind CSS*
