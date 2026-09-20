# AI Resume Screening System

An AI-powered resume screening application that analyzes resumes against hiring requirements and presents the results through a modern web dashboard.

The project combines:

- **C++** for the core resume/job screening logic
- **Node.js + Express** for the web backend
- **Google Gemini** for AI-based resume analysis
- **HTML, CSS and JavaScript** for the frontend dashboard
- **Chart.js** for visual analytics
- **PDF parsing** for extracting text from uploaded PDF resumes

---

## Features

### Resume Upload
- Drag-and-drop resume upload
- File selection from the browser
- PDF and text resume processing
- Upload validation on the frontend

### AI Resume Analysis
The Node.js backend sends extracted resume text to Google Gemini and receives structured analysis including:

- Overall resume score
- Recommendation
- Confidence score
- Matched skills
- Missing skills
- Skill-category analysis
- Resume strengths
- Resume weaknesses
- Improvement advice

### Interactive Dashboard
The frontend displays:

- Overall match score
- Recommendation badge
- Confidence score
- Processing time
- Skill distribution chart
- Category match chart
- Matched and missing skills
- AI-generated resume summary
- Strengths, weaknesses and recruiter advice

### C++ Screening Engine
The project also contains a standalone C++ screening engine that can:

1. Load a resume from a text file
2. Load job requirements
3. Compare required skills with resume skills
4. Calculate a skill-match percentage
5. Generate a recommendation
6. Save screening results as JSON

---

## Project Architecture

```text
                    ┌─────────────────────┐
                    │   Web Browser       │
                    │ HTML/CSS/JavaScript │
                    └──────────┬──────────┘
                               │
                         POST /screen
                               │
                               ▼
                    ┌─────────────────────┐
                    │ Node.js + Express   │
                    │      Backend        │
                    └──────────┬──────────┘
                               │
                  ┌────────────┴────────────┐
                  │                         │
                  ▼                         ▼
          ┌───────────────┐        ┌────────────────┐
          │ PDF/Text      │        │ Google Gemini  │
          │ Extraction    │        │ AI Analysis    │
          └───────────────┘        └────────────────┘
                                         │
                                         ▼
                              Structured JSON Result
                                         │
                                         ▼
                              ┌────────────────────┐
                              │ Dashboard + Charts │
                              └────────────────────┘


       Standalone C++ Screening Engine
       ─────────────────────────────────

       Resume ──► Resume Parser
                        │
       Job ─────► Job Parser
                        │
                        ▼
                Screening Engine
                        │
                        ▼
              Screening Result
                        │
                        ▼
                    result.json
```

> **Important:** The current web `/screen` endpoint performs its AI analysis directly through the Node.js/Gemini backend. The C++ screening engine is a separate standalone component included in the project.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, JavaScript |
| UI Icons | Lucide |
| Charts | Chart.js |
| Backend | Node.js |
| Web Framework | Express.js |
| File Upload | Multer |
| PDF Extraction | pdf-parse |
| AI | Google Gemini API |
| C++ Engine | C++ |
| Data Format | JSON / TXT |
| Styling | Custom CSS with dark/light themes |

---

## Project Structure

```text
ai_resume_screening/
│
├── backend/
│   ├── AIHelper.cpp
│   ├── AIHelper.h
│   ├── Job.cpp
│   ├── Job.h
│   ├── Resume.cpp
│   ├── Resume.h
│   ├── ScreeningEngine.cpp
│   ├── ScreeningEngine.h
│   ├── ScreeningResult.cpp
│   ├── ScreeningResult.h
│   ├── main.cpp
│   └── main.exe
│
├── data/
│   ├── jobs/
│   │   └── software_engineer.txt
│   │
│   ├── resumes/
│   │   ├── alice.txt
│   │   ├── bob.txt
│   │   ├── emma.txt
│   │   ├── john.txt
│   │   ├── priya.txt
│   │   └── rahul.txt
│   │
│   ├── results/
│   │   └── result.json
│   │
│   └── skills.txt
│
├── frontend/
│   ├── index.html
│   ├── script.js
│   └── style.css
│
├── server/
│   ├── server.js
│   ├── package.json
│   └── package-lock.json
│
├── package.json
└── package-lock.json
```

---

## Requirements

### For the Web Application

Install:

- **Node.js 18+**
- npm
- A Google Gemini API key

The Gemini SDK used by the server requires a modern Node.js version.

### For the C++ Engine

Install a C++ compiler such as:

- MinGW / g++
- GCC
- Visual Studio C++ compiler

---

# Installation

## 1. Clone or Download the Project

```bash
git clone <your-repository-url>
cd ai_resume_screening
```

If you downloaded the ZIP file, extract it and open the project folder in VS Code.

---

## 2. Install Backend Dependencies

Open a terminal inside the `server` directory:

```bash
cd server
npm install
```

This installs the required packages:

- express
- cors
- dotenv
- multer
- pdf-parse
- @google/generative-ai

---

## 3. Configure the Gemini API Key

Create a file named:

```text
server/.env
```

Add:

```env
GEMINI_API_KEY=your_gemini_api_key_here
```

Do **not** commit your API key to GitHub.

Add this to `.gitignore`:

```gitignore
.env
node_modules/
server/uploads/
```

---

## 4. Start the Web Application

From the `server` directory:

```bash
npm start
```

You should see:

```text
Server running on http://localhost:3000
```

Open your browser and visit:

```text
http://localhost:3000
```

---

# How to Use

### Step 1
Open the application in your browser.

### Step 2
Upload a resume using the upload area.

Supported reliably by the current backend:

```text
PDF
TXT
```

### Step 3
Click:

```text
Screen Resume
```

### Step 4
The backend extracts the resume text and sends it to Gemini for analysis.

### Step 5
The dashboard displays:

- Resume score
- Recommendation
- Confidence
- Processing time
- Matched skills
- Missing skills
- Skill charts
- AI summary
- Strengths
- Weaknesses
- Recruiter advice

---

# C++ Screening Engine

The C++ component provides a rule-based skill matching system.

## Job Definition

Example:

```text
Job Title: Software Engineer

Required Skills:
C++
OOP
SQL
Git
Problem Solving

Minimum Score: 60
```

## Screening Logic

For every required job skill, the engine checks whether the same skill exists in the resume.

The score is calculated as:

```text
Score = (Matched Skills / Required Skills) × 100
```

### Recommendation Rules

| Score | Recommendation |
|---:|---|
| 80–100 | Highly Recommended |
| 60–79 | Recommended |
| 40–59 | Consider |
| Below 40 | Rejected |

For example, if a job requires 5 skills and a resume contains all 5:

```text
5 / 5 × 100 = 100%
```

---

# Running the C++ Engine

Navigate to the backend:

```bash
cd backend
```

If you need to compile it:

```bash
g++ main.cpp Resume.cpp Job.cpp ScreeningEngine.cpp ScreeningResult.cpp AIHelper.cpp -o main
```

Then run:

```bash
./main
```

On Windows:

```bash
main.exe
```

The program allows a resume to be selected and produces a screening result.

The output is saved to:

```text
data/results/result.json
```

---

# Example Result

```json
{
  "score": 100,
  "recommendation": "Highly Recommended",
  "matchedSkills": [
    "C++",
    "OOP",
    "SQL",
    "Git",
    "Problem Solving"
  ],
  "missingSkills": [],
  "aiSummary": ""
}
```

---

# API

## POST `/screen`

Uploads and analyzes a resume.

### Request

Multipart form-data:

```text
resume: <resume file>
```

### Example

```javascript
const formData = new FormData();
formData.append("resume", file);

const response = await fetch("/screen", {
    method: "POST",
    body: formData
});

const result = await response.json();
```

### Response

The AI backend returns structured JSON containing fields such as:

```json
{
  "overallScore": 75,
  "recommendation": "Shortlist",
  "confidence": 92.5,
  "processingTime": 1.5,
  "matchedSkills": [],
  "missingSkills": [],
  "skillsData": {
    "radar": {
      "labels": [],
      "values": []
    },
    "bar": {
      "labels": [],
      "values": []
    }
  },
  "aiSummary": {
    "overall": "",
    "strengths": [],
    "weaknesses": [],
    "advice": ""
  }
}
```

---

# Frontend Highlights

The dashboard includes:

- Responsive two-column layout
- Glassmorphism UI
- Dark mode
- Light mode
- Drag-and-drop upload
- Loading skeleton
- Animated score
- Interactive charts
- Skill chips
- AI insights
- Toast notifications

The theme preference is stored in browser `localStorage`.

---

# Data Files

### `data/jobs/`

Contains job descriptions and required skills.

### `data/resumes/`

Contains sample text-based resumes for testing the C++ engine.

### `data/results/`

Stores generated C++ screening results.

### `data/skills.txt`

Contains the project's supported skill vocabulary.

---

# Security Notes

For production use:

1. Never hard-code API keys in source code.
2. Store `GEMINI_API_KEY` in environment variables.
3. Add `.env` to `.gitignore`.
4. Restrict uploaded file size.
5. Validate file contents, not only extensions.
6. Store uploaded files outside publicly accessible directories.
7. Sanitize uploaded filenames.
8. Add authentication and authorization before deploying publicly.
9. Consider rate limiting the `/screen` endpoint.
10. Do not store sensitive resume information longer than necessary.

---

# Current Limitations

- The C++ matcher uses exact skill-string matching, so variations such as `Object Oriented Programming` and `OOP` are not automatically treated as identical.
- The web backend currently extracts text from PDFs and reads other uploaded files as UTF-8 text. Although the frontend allows `.doc` and `.docx`, dedicated Word-document parsing is not currently implemented.
- The C++ engine and the Gemini-powered web screening flow are currently separate components.
- AI results depend on the Gemini model and the quality/content of the uploaded resume.
- The application is intended as a project/demo system and should not be treated as the sole basis for real hiring decisions.

---

# Future Enhancements

Possible improvements include:

- DOCX parsing
- OCR for scanned resumes
- Semantic skill matching
- Resume-to-job similarity using embeddings
- Multiple job descriptions
- Candidate ranking dashboard
- Recruiter authentication
- Database integration
- Resume history
- Export reports as PDF
- Improved C++/Node.js integration
- Bias and fairness auditing
- Duplicate resume detection
- Advanced ATS keyword analysis

---

# Learning Outcomes

This project demonstrates practical concepts in:

- Object-Oriented Programming
- C++ file handling
- Classes and objects
- Vectors and string processing
- Algorithmic skill matching
- JSON generation
- REST APIs
- Node.js backend development
- File uploads
- PDF text extraction
- Generative AI integration
- Frontend development
- Data visualization
- Responsive UI design

---

# Author

**AI Resume Screening System**

Developed as an academic/project implementation demonstrating the integration of C++, web technologies, and Generative AI.

---

## License

This project is intended for educational and demonstration purposes. Add an appropriate open-source license if you plan to distribute the project publicly.
