# AI Speech & Text Translator

A desktop translator supporting 100+ languages via voice and text input, with correct handling and database logging of non-Latin scripts including Urdu and Arabic.

---

## Overview

Dual-mode translation — type text or speak into your microphone — with every translation logged to a local MySQL database. A deliberate focus was ensuring non-Latin scripts display correctly in the GUI and store accurately using UTF-8 encoding throughout.

---

## Tech Stack

| | |
|---|---|
| **Language** | Python |
| **GUI** | Tkinter |
| **Speech Recognition** | Google Speech Recognition API |
| **Translation** | Googletrans API |
| **Database** | MySQL |

---

## Features

- Voice input via microphone — transcribed then translated
- Text input directly in the GUI
- 100+ languages supported
- Urdu, Arabic, and other non-Latin scripts display and store correctly
- Translation history logged to MySQL

---

## How It Works

### Voice mode
Microphone → SpeechRecognition → Google Speech API → Googletrans → Output → MySQL log

### Text mode
Typed input → Googletrans → Output → MySQL log

---

## Setup & Run

```bash
pip install -r requirements.txt
python main.py
```

**requirements.txt**
SpeechRecognition

googletrans==4.0.0rc1

mysql-connector-python

pyaudio

### Database setup
```sql
CREATE DATABASE translator_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
USE translator_db;
CREATE TABLE translations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    source_language VARCHAR(50),
    target_language VARCHAR(50),
    input_text TEXT CHARACTER SET utf8mb4,
    output_text TEXT CHARACTER SET utf8mb4,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Update `database.py` with your MySQL credentials.

---

## Testing

- **Regression testing** — re-running passing cases after each change to catch regressions
- **Random testing** — unexpected inputs (mixed scripts, empty strings, punctuation) to find edge cases
- **Oracle-based testing** — comparing output against a known-correct reference to verify accuracy

---

**University:** COMSATS University Islamabad, Wah Campus
