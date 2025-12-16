
---

# Safe Email Generator (Synthetic/Test Data)

## 1. Overview

**Safe Email Generator** is a desktop GUI application written in Python using Tkinter.
It generates **synthetic email addresses** for testing, development, and demonstration purposes.

The software is explicitly designed to **avoid real personal data**:

* Names are fictional and syllable-based
* Default domains are RFC-reserved example domains
* No real name lists or external data sources are used

The application supports **reproducible generation** via seeds, **deduplication**, and **structured export** to multiple formats.

---

## 2. Intended Use

This software is intended for:

* Software testing (forms, user databases, email validation)
* QA environments
* Demos and mock data generation
* Educational purposes

**Not intended for:**

* Generating real user data
* Sending emails
* Marketing or outreach
* Use with third-party domains without ownership

---

## 3. Key Features

### 3.1 Name Management

* Manual entry of specific names
* Automatic fictional name generation
* Seed-based reproducibility for names
* Append or replace existing name lists
* Case-insensitive deduplication

### 3.2 Email Generation

* Multiple configurable username patterns
* Randomized numeric suffixes
* Optional lowercase normalization
* Optional uniqueness enforcement
* Independent random seed for email generation

### 3.3 Domain Handling

* Safe default domains provided
* Custom domain input supported
* Domain format validation via regex

### 3.4 Output & Export

* Plain text email output
* Clipboard copy
* Save as `.txt`
* Structured exports:

  * CSV
  * JSON
  * SQL (CREATE TABLE + INSERT)

---

## 4. Architecture & Design

### 4.1 Application Structure

* **GUI Framework:** Tkinter
* **Main Class:** `App(tk.Tk)`
* **Execution Model:** Single-process, event-driven GUI
* **State Handling:** In-memory lists (no persistence layer)

### 4.2 Core Components

| Component           | Responsibility                 |
| ------------------- | ------------------------------ |
| `fictional_name()`  | Generates synthetic names      |
| `render_pattern()`  | Builds usernames from patterns |
| `slug()`            | Normalizes name parts          |
| `generate_names()`  | Creates fictional names        |
| `generate_emails()` | Main email generation logic    |
| `export_*()`        | Structured export handlers     |

---

## 5. Username Pattern System

Supported patterns include:

* `{first}.{last}`
* `{first}{last}`
* `{f}{last}`
* `{first}{l}`
* `{last}.{first}`
* `{first}_{last}`
* `{first}-{last}`
* `{first}.{last}{n2}`
* `{first}{last}{n3}`

Where:

* `f` / `l` = first letter
* `n2` = 2-digit random number
* `n3` = 3-digit random number

Patterns can be individually enabled or disabled via the GUI.

---

## 6. Data Validation & Safety

* Names must contain alphabetic characters
* Domains must match a valid domain regex
* Usernames are sanitized to `[a-z0-9._-]`
* Duplicate emails are optionally prevented
* SQL export escapes single quotes safely

---

## 7. Export Formats

### 7.1 CSV

* Columns: `name, email, domain, pattern, username`
* Proper CSV quoting
* UTF-8 encoded

### 7.2 JSON

* List of objects
* Pretty-printed
* UTF-8, non-ASCII preserved

### 7.3 SQL

* Generates table definition
* Bulk `INSERT INTO` statements
* Compatible with SQLite / PostgreSQL-style SQL

---

## 8. Requirements

### 8.1 Runtime Requirements

| Requirement | Version / Notes                        |
| ----------- | -------------------------------------- |
| Python      | ≥ 3.8                                  |
| Tkinter     | Required (usually bundled with Python) |
| OS          | Windows, Linux, macOS                  |

**Linux note:**
Tkinter may require manual installation:

```bash
sudo apt install python3-tk
```

---

### 8.2 Python Standard Library Dependencies

The application uses **only standard library modules**:

* `tkinter`
* `random`
* `re`
* `json`
* `datetime`
* `typing`

No third-party packages are required.

---

### 8.3 Hardware Requirements

* Minimal CPU usage
* RAM usage scales with generated entries
* Practical upper bound: ~200,000 emails per run (validated in code)

---

## 9. Installation & Execution

1. Ensure Python 3 is installed
2. Ensure Tkinter is available
3. Run the application:

```bash
python3 safe_email_generator.py
```

The GUI launches immediately; no configuration files are required.

---

## 10. Limitations

* GUI-only (no CLI mode)
* No persistence between sessions
* No email validation beyond syntax
* No internationalized domain support (IDN)
* No concurrency or background processing

---

## 11. Security & Compliance Notes

* Generates **synthetic data only**
* No network access
* No file access beyond user-selected exports
* Safe for GDPR-compliant test environments when used as intended

---

## 12. License & Usage Notes

* Intended for internal, testing, or educational use
* Users are responsible for ensuring domains used are owned or reserved
* Generated data should never be mistaken for real personal data

---

