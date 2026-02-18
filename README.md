# QuizCreator

QuizCreator is a modular quiz generation system that separates content, transformation logic, and frontend execution.

Quiz data is authored in Excel, transformed into structured JSON, cleaned and injected into JavaScript, and then rendered dynamically in the browser.

- Keep quiz content editable outside code
- Keep transformation logic modular
- Keep the frontend data-driven
- Avoid hardcoded question flows

---

## System Overview

The quiz system is structured in three clear layers:

1. Content Layer (Excel Workbook)
2. Transformation Layer (Python Pipeline)
3. Frontend Layer (HTML + JavaScript)

The HTML pages load core JavaScript modules.
Those modules access a shared JSON/JS dataset containing all quiz content.

This separation of structure, logic, and content allows flexible updates and easy maintenance.

---

## What It Does

QuizCreator allows you to:

- Define custom quizzes in Excel
- Convert structured Excel sheets into JSON
- Clean and normalize quiz data
- Inject quiz data into JavaScript
- Dynamically render quizzes in the browser
- Provide instant per-question feedback
- Generate end-of-quiz performance summaries

Every update follows the same predictable pipeline:

1. Enter questions in Excel
2. Run transformation script
3. Open the quiz in the browser

---

## Full Transformation Pipeline

Running the update script performs:

- Excel → JSON conversion
- Sheet consolidation into structured records
- Data cleaning and normalization
- Multi-answer splitting
- Grouping by module
- Wrapping output in a JavaScript variable
- Exporting cleaned JS and JSON files

Configuration is controlled via:

- `IMPORT_CFG`
- `CLEAN_CFG`

All behaviour is defined through configuration rather than hardcoded logic.

---

## Detailed Workflow

### Step 1 — Add Custom Questions and Answers

Enter your quiz content into the Excel workbook.

Each row includes:

- Question
- Multiple choice answers
- Correct answer
- Short explanation

Each sheet represents a quiz module.

---

### Step 2 — Update the Webpage Content

Run:

```bash
python3 Python-Update-Webpage.py
```

This script:

- Reads the Excel workbook
- Combines all module sheets into a single JSON structure
- Converts questions, answers, and metadata into structured records
- Cleans and restructures data
- Splits multi-answer fields
- Groups questions by module
- Wraps the result into a JavaScript variable
- Exports updated HTML, JSON, and JS files used by the quiz interface

---

### Step 3 — Launch the Quiz Selector

Open:

```
index.html
```

Users can:

- Select quizzes
- Navigate questions
- Receive instant feedback
- Review results

---

### Step 4 — Submit and Check Answers

After each question:

- Correct answers are highlighted
- Explanations are displayed

---

### Step 5 — Review Quiz Summary

Click **Submit Quiz** to:

- See total correct answers
- Review incorrect responses
- Access explanation references

---

### Step 6 — Build and Load Custom Quizzes

To create a new quiz:

1. Create a new Excel file using the same structure
2. Update:

```python
IMPORT_CFG['excel_file']
```

3. If needed, adjust:

- `sheet_names`
- `start_row`
- Output filenames in `IMPORT_CFG`
- Cleaner output names in `CLEAN_CFG`

The system adapts automatically.

---

## Architecture Principles

- Data-driven rendering
- Single-responsibility transformation stages
- Configuration-controlled execution
- Predictable pipeline behaviour
- No embedded quiz logic inside HTML
- Clear separation of content, transformation, and rendering

---

## Conceptual Architecture

```
Excel Workbook
        ↓
Python Import Layer
        ↓
Raw JSON Dataset
        ↓
Cleaner / Normalizer
        ↓
JavaScript Injection
        ↓
Dynamic Frontend Rendering
```

Content, logic, and UI remain fully decoupled.

---

## Run

To serve locally:

```bash
python3 -m http.server
```

Then open:

```
http://localhost:8000
```

Or open `index.html` directly in a browser.


## License

MIT License.

Anyone is free to use, modify, distribute, or improve this code.
