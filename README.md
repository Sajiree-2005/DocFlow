<div align="center">

# DOCFLOW

### **From manuscript chaos → structured, publication-ready DOCX.**

**An offline ML + rule-based document intelligence engine for automatic manuscript formatting.**

<br>

[![Python](https://img.shields.io/badge/Python-3.x-3776AB?style=flat-square&logo=python&logoColor=white)](#-technology)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-Random%20Forest-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)](#-machine-learning)
[![DOCX](https://img.shields.io/badge/DOCX-OOXML-2B579A?style=flat-square&logo=microsoftword&logoColor=white)](#-document-processing)
[![Offline](https://img.shields.io/badge/Processing-Local%20%26%20Offline-111827?style=flat-square)](#-privacy--offline-first)
[![Word Add-in](https://img.shields.io/badge/Microsoft%20Word-Add--in-2B579A?style=flat-square&logo=microsoftword&logoColor=white)](#-microsoft-word-add-in)

<br>

> **DocFlow reads the structure of a manuscript, understands what each element is, formats it according to a publication specification, and verifies that the content survived the transformation.**

</div>

---

## ◈ Index

**Jump directly to any part of the project:**

| | Section | What you'll find |
|---|---|---|
| 🎯 | [The Problem](#-the-problem) | Why manuscript formatting is still manual |
| ✦ | [What DocFlow Does](#-what-docflow-does) | Product capabilities |
| ⚡ | [Quick Look](#-quick-look) | The complete processing flow |
| 🧠 | [Machine Learning](#-machine-learning) | Features, classes and evaluation |
| 🛡️ | [Hybrid Intelligence](#-hybrid-intelligence-ml--rules) | Why ML and deterministic rules work together |
| 📐 | [Formatting Engine](#-formatting-engine) | Publication specification |
| 🔐 | [Integrity Validation](#-integrity-validation) | How output correctness is checked |
| 📊 | [Performance](#-performance) | Scale and throughput results |
| 🖥️ | [Word Add-in](#-microsoft-word-add-in) | Run DocFlow inside Word |
| 🌐 | [Standalone Mode](#-standalone-browser-mode) | Process DOCX without Word |
| 📴 | [Privacy](#-privacy--offline-first) | Local processing architecture |
| 🏗️ | [Architecture](#-architecture) | System design |
| 🧰 | [Technology](#-technology) | Full stack |
| 📁 | [Repository](#-repository-map) | Codebase structure |
| 🚀 | [Installation](#-quick-start) | Get it running |
| 🧪 | [Testing](#-testing--evaluation) | Samples, comparison and scale tests |
| 📦 | [Packaging](#-packaging) | Standalone executable |
| 🛣️ | [Roadmap](#-roadmap) | Planned extensions |

---

# 🎯 The Problem

A manuscript can be **content-complete but formatting-inconsistent**.

A long document may contain titles, authors, chapter headings, subheadings, body paragraphs, tables, figures, captions, references and lists — all mixed together and formatted differently.

Traditional cleanup means manually finding those elements and repeatedly correcting:

- typography
- spacing
- indentation
- alignment
- margins
- heading hierarchy
- figure/caption presentation
- table formatting
- references

For large manuscripts, this becomes a repetitive **structure-recognition problem**, not simply a font-changing problem.

### DocFlow's approach

Instead of asking the user to manually identify every element:

```text
                    RAW MANUSCRIPT
                          │
                          ▼
                 ┌─────────────────┐
                 │ Understand DOCX │
                 └────────┬────────┘
                          ▼
                 ┌─────────────────┐
                 │ Identify roles  │
                 └────────┬────────┘
                          ▼
                 ┌─────────────────┐
                 │ Apply rules     │
                 └────────┬────────┘
                          ▼
                 ┌─────────────────┐
                 │ Validate output │
                 └────────┬────────┘
                          ▼
                 PUBLICATION-READY DOCX
```

---

# ✦ What DocFlow Does

### One engine. Two ways to use it.

| Capability | What happens |
|---|---|
| 🧠 **Structure Recognition** | Understands the semantic role of document elements |
| 🤖 **ML Classification** | Predicts one of 10 manuscript element classes |
| 🛡️ **Rule Verification** | Overrides predictions when document structure is explicit |
| 🎨 **Automatic Typesetting** | Applies a fixed publication specification |
| 📋 **Table & Figure Handling** | Treats tables, images and captions as structural elements |
| 📚 **Reference Detection** | Identifies reference-style paragraphs |
| 🔍 **Integrity Checks** | Verifies content and structure after formatting |
| 👁️ **Before/After Proof** | Provides a visual comparison of raw vs formatted output |
| 📴 **Local Processing** | Core parsing, classification and formatting happen locally |
| 📝 **Word Integration** | Runs from a Microsoft Word task pane |
| 🌐 **Standalone Mode** | Processes `.docx` files from Word or LibreOffice |
| 📦 **Executable Build** | Can be packaged with PyInstaller |

---

# ⚡ Quick Look

## What happens when you click **Format Manuscript**?

```text
┌───────────────────────────────────────────────────────────────┐
│                         INPUT .DOCX                           │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  01  PARSE                                                    │
│      Read paragraphs + tables in document order                │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  02  EXTRACT                                                  │
│      Convert document structure into 16 measurable features   │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  03  CLASSIFY                                                 │
│      Random Forest predicts the semantic role of each element │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  04  VERIFY                                                   │
│      Deterministic rules correct explicit structural cases    │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  05  FORMAT                                                   │
│      Apply publication typography + page layout               │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│  06  VALIDATE                                                 │
│      Check OOXML, text, tables, labels and formatting         │
└──────────────────────────────┬────────────────────────────────┘
                               │
                               ▼
┌───────────────────────────────────────────────────────────────┐
│                    FORMATTED .DOCX                            │
└───────────────────────────────────────────────────────────────┘
```

---

# 🧠 Machine Learning

DocFlow does not treat a manuscript as a bag of words.

For each relevant paragraph or table, the parser builds a **16-feature structural representation**.

### Feature signals include

```text
Typography
├── Font size
├── Bold / italic
└── Word style

Layout
├── Alignment
├── Left indentation
├── First-line indentation
├── Paragraph spacing
└── Line spacing

Content shape
├── Word count
├── Capitalization patterns
└── Numbering patterns

Document context
├── Position in document
├── Image presence
└── Table presence
```

These features are passed to the trained classifier in batches.

---

## 10 document classes

```text
┌────────────────────┬────────────────────┐
│ TITLE              │ AUTHOR             │
├────────────────────┼────────────────────┤
│ CHAPTER HEADING    │ SUBHEADING         │
├────────────────────┼────────────────────┤
│ BODY PARAGRAPH     │ TABLE              │
├────────────────────┼────────────────────┤
│ FIGURE             │ CAPTION            │
├────────────────────┼────────────────────┤
│ REFERENCE          │ LIST               │
└────────────────────┴────────────────────┘
```

---

## Model Evaluation

The current evaluation set contains **182 samples**.

| Metric | Result |
|---|---:|
| **Test Accuracy** | **96.7%** |
| **Cross-Validation Accuracy** | **99.0% ± 1.3%** |
| **Evaluation Samples** | **182** |

### Class-level evaluation

The current report shows perfect test precision/recall for most structural classes, with the main confusion occurring between **Chapter Heading** and **Subheading**.

The repository includes the generated confusion matrix:

![DocFlow confusion matrix](model/artifacts/confusion_matrix.png)

> These metrics describe the current training/evaluation dataset and should not be interpreted as a guarantee for arbitrary unseen document formats.

---

# 🛡️ Hybrid Intelligence: ML + Rules

A purely ML-driven formatter is not enough.

Some structures are explicit in the DOCX itself.

For example:

```text
Word table exists?
        │
       YES
        ▼
     TABLE
```

```text
Paragraph contains an image?
        │
       YES
        ▼
     FIGURE
```

DocFlow therefore combines:

### 🤖 Machine Learning

Useful for recognizing patterns from formatting and document context.

### ⚙️ Deterministic Rules

Useful when the document structure provides strong evidence.

```text
              DOCUMENT
                  │
                  ▼
        ┌───────────────────┐
        │  ML CLASSIFIER    │
        └─────────┬─────────┘
                  │
                  ▼
        ┌───────────────────┐
        │ RULE VERIFICATION │
        └─────────┬─────────┘
                  │
                  ▼
          FINAL STRUCTURE
```

This keeps the system more predictable than relying on a model alone.

---

# 📐 Formatting Engine

Once the structure is known, DocFlow applies a deterministic publication specification.

## Body text

| Property | Specification |
|---|---|
| Font | Times New Roman |
| Size | 12 pt |
| Alignment | Justified |
| Line spacing | 1.5 |
| First-line indent | 1.27 cm |

## Page layout

| Margin | Value |
|---|---:|
| Top | 1.52 cm |
| Bottom | 1.52 cm |
| Left | 1.97 cm |
| Right | 1.96 cm |

## Structural formatting

| Element | Formatting |
|---|---|
| **Title** | 20 pt, bold, centered |
| **Author** | 13 pt, italic, centered |
| **Chapter Heading** | 16 pt, bold |
| **Subheading** | 12 pt, bold |
| **Body Paragraph** | 12 pt, justified |
| **Figure** | 11 pt, centered |
| **Caption** | 10 pt, italic, centered |
| **Reference** | 10 pt, justified |
| **List** | 12 pt |
| **Table** | 11 pt, centered, table grid |

The formatter writes the resulting properties directly into the DOCX structure using `python-docx`.

---

# 🔐 Integrity Validation

**Formatting is allowed to change presentation. It is not allowed to silently change the manuscript.**

After formatting, DocFlow validates:

```text
             OUTPUT DOCX
                  │
       ┌──────────┼──────────┐
       ▼          ▼          ▼
    OOXML       CONTENT    STRUCTURE
    valid?      intact?     intact?
       │          │          │
       └──────────┼──────────┘
                  ▼
              VALIDATED
```

The validation layer checks:

- ✅ Output is valid OOXML
- ✅ Paragraph text is preserved
- ✅ Paragraph ordering is preserved
- ✅ Table count is preserved
- ✅ Table cell content is preserved
- ✅ Every processed element receives a classification
- ✅ Formatting is applied to processed elements

This gives the pipeline a clear contract:

> **Understand → transform presentation → verify preservation.**

---

# 📊 Performance

DocFlow was profiled against a large synthetic manuscript.

| Metric | Result |
|---|---:|
| **Elements processed** | **4,675** |
| **Wall-clock time** | **5.95 s** |
| **Throughput** | **785.3 elements/s** |
| **Peak memory** | **257.6 MB** |
| **Validation** | **PASSED** |

### What was processed?

```text
Body Paragraph       2935
Chapter Heading       435
Subheading            360
Caption               311
Reference             237
List                  229
Table                 168
```

The profiler and scale-test scripts are included in the repository so these numbers can be reproduced.

---

# 🖥️ Microsoft Word Add-in

DocFlow can run **inside Word** through a task pane.

```text
┌──────────────────────────────┐
│         MICROSOFT WORD       │
│                              │
│  Manuscript                  │
│  ──────────────────────────  │
│                              │
│             ┌──────────────┐ │
│             │   DOCFLOW    │ │
│             │              │ │
│             │ Format       │ │
│             │ Manuscript   │ │
│             │              │ │
│             │ Proof  ◀───▶ │ │
│             │              │ │
│             │ ✓ Validated  │ │
│             └──────────────┘ │
└──────────────────────────────┘
```

### The add-in flow

1. Open the manuscript in Word
2. Open the DocFlow task pane
3. Click **Format Manuscript**
4. DocFlow sends the document to the local engine
5. Review the before/after proof
6. Check the processing summary
7. Download the formatted `.docx`

The add-in and standalone interface use the **same underlying engine**.

---

# 🌐 Standalone Browser Mode

No Word add-in required.

```text
        SELECT .DOCX
             │
             ▼
       LOCAL DOCFLOW
             │
      ┌──────┴──────┐
      ▼             ▼
    RAW           FORMATTED
      │             │
      └──────┬──────┘
             ▼
       BEFORE / AFTER
           PROOF
             │
             ▼
      DOWNLOAD .DOCX
```

The standalone page accepts `.docx` files created with:

- Microsoft Word
- LibreOffice Writer

This makes it useful both as a standalone workflow and as a fallback when Word add-in sideloading is unavailable.

---

# 📴 Privacy & Offline-First

The **document-processing engine is local**.

```text
                    YOUR MACHINE
┌──────────────────────────────────────────┐
│                                          │
│  .DOCX                                   │
│    │                                     │
│    ▼                                     │
│  python-docx                             │
│    │                                     │
│    ▼                                     │
│  Feature Extraction                      │
│    │                                     │
│    ▼                                     │
│  Local ML Model                           │
│    │                                     │
│    ▼                                     │
│  Rules + Formatting                      │
│    │                                     │
│    ▼                                     │
│  Validation                              │
│    │                                     │
│    ▼                                     │
│  Formatted .DOCX                         │
│                                          │
└──────────────────────────────────────────┘
```

The core engine does **not** require a generative AI model, LLM or cloud document-processing service.

### One important distinction

The Word add-in loads Microsoft's `office.js` library from Microsoft's hosted URL because Office.js needs to communicate with the Word host.

That is separate from the document-processing engine:

**Office.js → Word integration**

**Local Python engine → parsing, ML, formatting and validation**

---

# 🏗️ Architecture

```text
                         ┌──────────────────────┐
                         │   MICROSOFT WORD     │
                         │      TASK PANE       │
                         └──────────┬───────────┘
                                    │
                                    │ HTTPS / localhost
                                    ▼
                         ┌──────────────────────┐
                         │    FLASK SERVER      │
                         │  Local REST API      │
                         └──────────┬───────────┘
                                    │
                                    ▼
             ┌──────────────────────────────────────────┐
             │             DOCFLOW ENGINE               │
             │                                          │
             │   DOCX Parser                            │
             │        ↓                                 │
             │   Feature Extraction                     │
             │        ↓                                 │
             │   ML Classifier                          │
             │        ↓                                 │
             │   Rule Verification                      │
             │        ↓                                 │
             │   Formatting Engine                      │
             │        ↓                                 │
             │   Integrity Validation                   │
             └────────────────────┬─────────────────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Formatted .DOCX │
                         └──────────────────┘
```

The standalone browser page connects to the same local server and processing engine.

---

# 🧰 Technology

| Layer | Technology |
|---|---|
| **Language** | Python |
| **Document model** | DOCX / OOXML |
| **DOCX processing** | `python-docx` |
| **ML** | scikit-learn |
| **Model** | Random Forest classifier |
| **Serialization** | Joblib |
| **Server** | Flask |
| **Word integration** | Office.js |
| **Frontend** | HTML / CSS / JavaScript |
| **Packaging** | PyInstaller |
| **Local HTTPS** | Self-signed development certificate |

---

# 📁 Repository Map

```text
DocFlow/
│
├── engine/
│   ├── docx_parser.py          # DOCX → structural features
│   ├── classifier_stub.py      # model inference + rule overrides
│   ├── formatting_engine.py    # publication formatting
│   ├── validation.py           # integrity validation
│   ├── main_pipeline.py        # pipeline orchestration
│   └── requirements.txt
│
├── model/
│   ├── train.ipynb             # training / evaluation notebook
│   ├── feature_spec.md         # feature contract
│   └── artifacts/
│       ├── classifier.joblib
│       ├── scaler.joblib
│       ├── training_data.csv
│       ├── evaluation_report.md
│       └── confusion_matrix.png
│
├── addin/
│   ├── manifest.xml             # Word add-in manifest
│   ├── taskpane.html            # Word task pane
│   ├── taskpane.js
│   ├── standalone.html          # browser mode
│   ├── standalone.js
│   ├── taskpane.css
│   └── assets/
│
├── server/
│   ├── app.py                   # local HTTPS server + API
│   └── certs.py                 # certificate generation
│
├── scripts/
│   ├── run_all_samples.py
│   ├── build_scale_test_doc.py
│   ├── profile_performance.py
│   ├── compare_before_after.py
│   └── compare_before_after_html.py
│
├── samples/
│   ├── manuscript_01.docx
│   ├── manuscript_01_formatted.docx
│   ├── ...
│   └── scale_test_manuscript.docx
│
├── deployment_delivery/
│   └── DEPLOYMENT.md
│
├── build_exe.py
├── trust_certificate.ps1
└── requirements.txt
```

---

# 🚀 Quick Start

## 1. Clone

```bash
git clone https://github.com/Jidnyasa-P/DocFlow.git
cd DocFlow
```

## 2. Create the environment

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

## 3. Install the engine dependencies

```bash
pip install -r engine/requirements.txt
```

> Keep the pinned `scikit-learn` version used by the trained model. If the model is retrained with a different version, update the dependency together with the model artifacts.

## 4. Format a sample manuscript

```bash
cd engine
python main_pipeline.py ../samples/manuscript_01.docx ../samples/manuscript_01_formatted.docx
```

The pipeline runs:

```text
PARSE → CLASSIFY → VERIFY → FORMAT → VALIDATE
```

---

# 🧪 Testing & Evaluation

## Run all samples

From the repository root:

```bash
python scripts/run_all_samples.py
```

## Generate a large test manuscript

```bash
python scripts/build_scale_test_doc.py --target-pages 400
```

## Profile performance

```bash
python scripts/profile_performance.py samples/scale_test_manuscript.docx --out performance_report.md
```

## Generate a before/after comparison

```bash
python engine/main_pipeline.py samples/manuscript_03.docx samples/manuscript_03_formatted.docx
python scripts/compare_before_after_html.py samples/manuscript_03.docx samples/manuscript_03_formatted.docx samples/manuscript_03_comparison.html
```

If LibreOffice and the required rendering utilities are available, the comparison can include rendered page images; otherwise the comparison falls back to formatting-oriented output.

---

# 📝 Running the Word Add-in

Install the Python environment first, then install Flask if needed:

```powershell
pip install flask
```

Start the local server:

```powershell
python server\app.py
```

The server exposes the local DocFlow application at:

```text
https://localhost:3000
```

### Word

Load:

```text
addin/manifest.xml
```

Then open a manuscript and use the **DocFlow** task pane.

Detailed setup, sideloading and troubleshooting instructions are available in:

```text
addin/ADDIN_README.md
```

---

# 🌐 Running Standalone Mode

With the server running, open:

```text
https://localhost:3000/app
```

Then:

1. Select a `.docx` manuscript
2. Wait for processing
3. Review the proof
4. Check validation
5. Download the formatted document

No Word add-in sideloading is required.

---

# 📦 Packaging

DocFlow can be packaged into a standalone Windows executable:

```powershell
pip install pyinstaller cryptography
python build_exe.py
```

The packaging workflow is documented in:

```text
deployment_delivery/DEPLOYMENT.md
```

---

# 🛣️ Roadmap

The current engine uses a fixed publication specification. Natural extensions include:

- [ ] Multiple publication templates
- [ ] Journal-specific formatting profiles
- [ ] Thesis/dissertation templates
- [ ] Conference/proceedings templates
- [ ] Custom formatting profiles
- [ ] Expanded document-structure classes
- [ ] More robust handling of complex DOCX layouts
- [ ] Additional citation/reference styles
- [ ] Cross-platform distribution
- [ ] Larger and more diverse evaluation datasets

---

# 🔬 Engineering Principles

DocFlow is intentionally built around a few principles:

### 01 — Structure before styling

The system first asks **"What is this element?"** and only then asks **"How should it look?"**

### 02 — ML where patterns matter

Formatting signals and document context are useful for recognizing semantic roles.

### 03 — Rules where certainty exists

Explicit DOCX structures should not be left to probability.

### 04 — Formatting should be reversible in principle

The engine changes presentation rather than rewriting manuscript content.

### 05 — Validate the output

A generated document is not considered successful simply because it opens. Its content and structure are checked after transformation.

---

<div align="center">

## DOCFLOW

### **Understand the document. Format the structure. Verify the result.**

`DOCX` · `ML` · `Rules` · `OOXML` · `Word Add-in` · `Local Processing`

<br>

**Built with Python · scikit-learn · python-docx · Flask · Office.js**

</div>
