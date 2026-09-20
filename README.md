# DocFlow

### Turn an unstructured manuscript into a publication-ready document — locally.

**DocFlow** is an offline ML-powered document formatting system that understands the structure of a `.docx` manuscript and automatically transforms it into a consistent, publication-ready format.

Instead of manually identifying titles, headings, paragraphs, references, captions, figures, tables, and lists, DocFlow analyzes the document structure, classifies each element, applies the appropriate formatting rules, validates the result, and produces a new `.docx` file.

> **Write the content. DocFlow handles the typesetting.**

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/scikit--learn-ML-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" />
  <img src="https://img.shields.io/badge/Word-Add--in-2B579A?style=for-the-badge&logo=microsoftword&logoColor=white" />
  <img src="https://img.shields.io/badge/Offline-First-111827?style=for-the-badge" />
  <img src="https://img.shields.io/badge/.DOCX-Supported-4285F4?style=for-the-badge" />
</p>

---

## ✦ Why DocFlow?

Formatting a long manuscript is more than changing fonts.

A real document contains different structural elements:

`Title` · `Author` · `Chapter` · `Subheading` · `Body` · `Table` · `Figure` · `Caption` · `Reference` · `List`

These elements need different formatting rules.

DocFlow automatically identifies these structures and applies a consistent publication specification — without rewriting the document's content.

### From this

```text
Raw manuscript
    ↓
Mixed fonts
    ↓
Inconsistent headings
    ↓
Irregular spacing
    ↓
Manual formatting
    ↓
Repeated corrections
```

### To this

```text
DOCX
 ↓
Structure Detection
 ↓
ML Classification
 ↓
Rule-based Verification
 ↓
Publication Formatting
 ↓
Integrity Validation
 ↓
Formatted DOCX
```

---

# ✨ What DocFlow Does

| Capability | Description |
|---|---|
| 🧠 **Document Structure Detection** | Identifies the semantic role of document elements |
| 🤖 **ML Classification** | Classifies content into 10 document categories |
| ⚙️ **Rule-Based Verification** | Applies deterministic structural checks on top of ML predictions |
| 📐 **Automatic Typesetting** | Applies consistent fonts, spacing, indentation, margins and alignment |
| 📊 **Table & Figure Handling** | Detects and formats tables, figures and captions separately |
| 📚 **Reference Formatting** | Recognizes reference-style content and applies dedicated formatting |
| 🔍 **Integrity Validation** | Checks that document content is preserved after formatting |
| 👁️ **Before / After Proof** | Visually compare the original and formatted manuscript |
| 📴 **Offline Processing** | Document processing happens locally |
| 📝 **Word Integration** | Runs directly inside Microsoft Word through a task pane |
| 🌐 **Standalone Mode** | Process `.docx` files without opening Word |
| 📦 **Distributable Build** | Can be packaged as a standalone executable |

---

# 🧠 How It Works

```text
                    ┌─────────────────────┐
                    │   Input .DOCX       │
                    └──────────┬──────────┘
                               │
                               ▼
                 ┌─────────────────────────┐
                 │  DOCX Parser            │
                 │  Structure + Features   │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │  ML Structure Classifier│
                 │  10 document classes    │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │ Rule-Based Verification │
                 │ Structural overrides    │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │  Formatting Engine      │
                 │  Publication Rules      │
                 └──────────┬──────────────┘
                            │
                            ▼
                 ┌─────────────────────────┐
                 │ Validation & Integrity  │
                 │ Checks                  │
                 └──────────┬──────────────┘
                            │
                            ▼
                     Publication-Ready DOCX
```

---

# 🔎 1. Document Understanding

DocFlow parses the underlying DOCX structure instead of treating the manuscript as plain text.

For every relevant paragraph or table, it extracts a **16-feature structural representation**, including:

- Font size
- Bold / italic state
- Alignment
- Left and first-line indentation
- Paragraph spacing
- Line spacing
- Capitalization patterns
- Numbering patterns
- Word count
- Position within the document
- Word style
- Image presence
- Table presence

This allows the system to reason about **how content is structured**, not just what the words say.

---

# 🤖 2. ML-Based Classification

The extracted features are passed to a trained scikit-learn classifier.

DocFlow recognizes **10 document element types**:

```text
Title
Author
Chapter Heading
Subheading
Body Paragraph
Table
Figure
Caption
Reference
List
```

The classifier processes document elements in **batches**, making the pipeline suitable for large manuscripts.

### Model evaluation

| Metric | Result |
|---|---:|
| Test Accuracy | **96.7%** |
| Cross-Validation Accuracy | **99.0% ± 1.3%** |
| Evaluation Samples | **182** |

> Evaluation results are based on the current training/evaluation dataset included in the repository.

---

# 🛡️ 3. ML + Rules Instead of ML Alone

DocFlow does not blindly trust the classifier.

A deterministic verification layer sits after ML classification and handles cases where document structure is explicit.

For example:

```text
Is it an actual Word table?
        ↓
      Yes
        ↓
      TABLE
```

```text
Does the paragraph contain an image?
        ↓
      Yes
        ↓
     FIGURE
```

This creates a practical combination:

**Machine learning for flexible structure recognition + deterministic rules for predictable document structures.**

---

# 🎨 4. Publication Formatting Engine

Once the document structure is identified, DocFlow applies formatting according to the element type.

### Body text

- Times New Roman
- 12 pt
- Justified alignment
- 1.5 line spacing
- 1.27 cm first-line indentation

### Page layout

- Top: 1.52 cm
- Bottom: 1.52 cm
- Left: 1.97 cm
- Right: 1.96 cm

### Structural elements

| Element | Formatting |
|---|---|
| Title | 20 pt, bold, centered |
| Author | 13 pt, italic, centered |
| Chapter Heading | 16 pt, bold |
| Subheading | 12 pt, bold |
| Body Paragraph | 12 pt, justified |
| Figure | 11 pt, centered |
| Caption | 10 pt, italic, centered |
| Reference | 10 pt, justified |
| List | 12 pt |
| Table | 11 pt, centered, table grid |

---

# 🔐 5. Content Integrity Comes First

Formatting should never mean rewriting.

Before returning the output, DocFlow validates the generated document.

The validation layer checks:

- ✅ Output is valid OOXML
- ✅ Paragraph text remains unchanged
- ✅ Paragraph ordering is preserved
- ✅ Table count is preserved
- ✅ Table cell content is preserved
- ✅ Every processed element receives a classification
- ✅ Formatting is actually applied

DocFlow focuses on changing **presentation**, not **content**.

---

# ⚡ Performance

DocFlow has also been tested against a large synthetic manuscript.

### Scale test

| Metric | Result |
|---|---:|
| Elements processed | **4,675** |
| Processing time | **5.95 s** |
| Throughput | **785.3 elements/s** |
| Peak memory | **257.6 MB** |
| Validation | **PASSED** |

The pipeline performs classification in batches rather than making one model call per document element, reducing processing overhead on large manuscripts.

---

# 🖥️ Use It Where You Work

DocFlow provides two interfaces using the same underlying processing engine.

## Microsoft Word Add-in

Run DocFlow directly inside Word.

```text
Open Manuscript
      ↓
Format Manuscript
      ↓
DocFlow processes the document
      ↓
Before / After Proof
      ↓
Download formatted DOCX
```

The Word task pane provides:

- One-click formatting
- Processing status
- Before/after comparison
- Element count
- Processing time
- Validation status
- Formatted `.docx` output

---

## Standalone Browser Mode

Don't want to use the Word add-in?

DocFlow also provides a standalone browser interface.

```text
Choose .docx
      ↓
Process locally
      ↓
Review before / after
      ↓
Download formatted .docx
```

It can process `.docx` files created using **Microsoft Word or LibreOffice Writer**.

---

# 📴 Privacy & Offline-First Architecture

One of DocFlow's core design decisions is keeping document processing local.

```text
             YOUR MACHINE
┌───────────────────────────────────────┐
│                                       │
│  DOCX                                 │
│   │                                   │
│   ▼                                   │
│  Parser                               │
│   │                                   │
│   ▼                                   │
│  ML Classifier                        │
│   │                                   │
│   ▼                                   │
│  Formatting Engine                    │
│   │                                   │
│   ▼                                   │
│  Validation                           │
│   │                                   │
│   ▼                                   │
│  Formatted DOCX                       │
│                                       │
└───────────────────────────────────────┘
```

The Python processing pipeline does not require a cloud AI service or LLM to analyze the manuscript.

> **Note:** The Word add-in loads Microsoft's `office.js` library to communicate with Word. The actual document parsing, classification, formatting and validation pipeline runs locally.

---

# 🏗️ Architecture

```text
                    ┌─────────────────────┐
                    │   Word Add-in       │
                    │   Task Pane         │
                    └──────────┬──────────┘
                               │
                    ┌──────────▼──────────┐
                    │ Local HTTPS Server  │
                    │ Flask               │
                    └──────────┬──────────┘
                               │
              ┌────────────────▼────────────────┐
              │         DocFlow Engine         │
              │                                │
              │  DOCX Parser                   │
              │       ↓                        │
              │  ML Classifier                 │
              │       ↓                        │
              │  Rule Verification             │
              │       ↓                        │
              │  Formatting Engine             │
              │       ↓                        │
              │  Validation                    │
              └────────────────┬───────────────┘
                               │
                               ▼
                     Publication-Ready DOCX
```

The standalone browser interface uses the same local engine.

---

# 🧰 Tech Stack

### Core

- Python
- `python-docx`
- NumPy
- scikit-learn
- Joblib

### Backend

- Flask
- Local HTTPS server
- REST API

### Document Processing

- Microsoft Word `.docx`
- OOXML
- python-docx

### Frontend

- HTML
- CSS
- JavaScript
- Microsoft Office.js

### Packaging

- PyInstaller
- Self-signed local HTTPS certificate

---

# 📁 Project Structure

```text
DocFlow/
│
├── engine/
│   ├── docx_parser.py
│   ├── classifier_stub.py
│   ├── formatting_engine.py
│   ├── validation.py
│   ├── main_pipeline.py
│   └── requirements.txt
│
├── model/
│   ├── train.ipynb
│   ├── feature_spec.md
│   └── artifacts/
│       ├── classifier.joblib
│       ├── scaler.joblib
│       ├── evaluation_report.md
│       └── confusion_matrix.png
│
├── addin/
│   ├── manifest.xml
│   ├── taskpane.html
│   ├── taskpane.js
│   ├── standalone.html
│   ├── standalone.js
│   ├── taskpane.css
│   └── assets/
│
├── server/
│   ├── app.py
│   └── certs.py
│
├── scripts/
│   ├── run_all_samples.py
│   ├── build_scale_test_doc.py
│   ├── profile_performance.py
│   ├── compare_before_after.py
│   └── compare_before_after_html.py
│
├── samples/
│
├── build_exe.py
├── trust_certificate.ps1
├── requirements.txt
└── README.md
```

---

# 🚀 Quick Start

## 1. Clone the repository

```bash
git clone https://github.com/Jidnyasa-P/DocFlow.git
cd DocFlow
```

## 2. Create a virtual environment

### Windows

```powershell
python -m venv venv
venv\Scripts\activate
```

### macOS / Linux

```bash
python -m venv venv
source venv/bin/activate
```

## 3. Install dependencies

```bash
pip install -r engine/requirements.txt
```

## 4. Run the local processing pipeline

```bash
cd engine
python main_pipeline.py ../samples/manuscript_01.docx ../samples/manuscript_01_formatted.docx
```

The pipeline will:

```text
Parse
  ↓
Classify
  ↓
Format
  ↓
Validate
  ↓
Generate DOCX
```

---

# 🧪 Run the Sample Suite

```bash
cd ..
python scripts/run_all_samples.py
```

The repository contains sample documents and formatted outputs for evaluating the system.

---

# 🖥️ Run the Word Add-in

Start the local server:

```powershell
python server\app.py
```

Then load the provided `addin/manifest.xml` into Word using the Office add-in sideloading workflow.

Once loaded:

```text
Open manuscript
      ↓
Open DocFlow
      ↓
Format Manuscript
      ↓
Review proof
      ↓
Download formatted document
```

For complete Word setup and sideloading instructions, see:

`addin/ADDIN_README.md`

---

# 🌐 Standalone Browser Mode

With the local server running, open the standalone application using the route configured by the server.

Then:

1. Choose a `.docx` manuscript
2. Let DocFlow process it
3. Review the before/after proof
4. Check validation status
5. Download the formatted `.docx`

---

# 📦 Packaging

DocFlow can be packaged into a standalone Windows distribution using PyInstaller.

```powershell
pip install pyinstaller cryptography
python build_exe.py
```

The generated distribution contains the application, processing engine, trained model and required runtime components.

---

# 🛣️ Future Directions

Potential extensions include:

- 📚 Multiple publication templates
- 🏛️ Journal-specific formatting profiles
- 🎓 Academic thesis formatting
- 📰 Conference and proceedings templates
- 🎨 Custom style presets
- 🧩 More advanced DOCX structure recognition
- 📑 Additional citation and reference styles
- 🔎 Improved handling of complex layouts
- 🖥️ Cross-platform packaging
- 📊 Expanded evaluation datasets

---

# 📊 Project Highlights

| | |
|---|---|
| **10** | Document Classes |
| **16** | Structural Features |
| **96.7%** | Test Accuracy |
| **99.0% ± 1.3%** | Cross-Validation Accuracy |
| **4,675** | Elements Processed |
| **785+ / sec** | Processing Throughput |
| **5.95 sec** | Large-Document Processing Time |

---

# 💡 Design Philosophy

> **Formatting should be structural, repeatable and verifiable — not a manual cleanup task.**

Rather than generating or rewriting manuscript content, DocFlow focuses on understanding document structure and applying deterministic presentation rules.

That separation keeps the system:

**Predictable → Local → Auditable → Reproducible**

---

# 📄 License

Add your preferred license here before making the repository public.

---

<p align="center">

### DocFlow

**From manuscript chaos to consistent typesetting.**

Built with Python · scikit-learn · python-docx · Flask · Office.js

</p>
