AI Speech & Text Translator

A bilingual desktop translator supporting 100+ languages via voice and text input, with correct handling and database logging of non-Latin scripts including Urdu and Arabic.


Overview

This desktop application provides dual-mode translation — you can either type text or speak into your microphone — and logs every translation to a local MySQL database. A deliberate design focus was ensuring non-Latin scripts (Urdu, Arabic, Chinese, etc.) display correctly in the GUI and are stored accurately in the database using UTF-8 encoding throughout.


Tech Stack

LanguagePythonGUITkinterSpeech RecognitionGoogle Speech Recognition API (SpeechRecognition)TranslationGoogletrans APIDatabaseMySQL


Features


Voice input — speak into the microphone; speech is transcribed then translated
Text input — type directly into the GUI
100+ languages — full language list supported by Googletrans
Non-Latin script support — Urdu, Arabic, Chinese, and other scripts display and store correctly
Translation history — every translation logged to MySQL with source language, target language, input, and output
Simple GUI — clean Tkinter interface with language selectors and input/output panels



Project Structure

ai-translator/
├── main.py                  # Entry point, GUI setup
├── translator.py            # Translation logic (Googletrans)
├── speech_handler.py        # Microphone input + Google Speech Recognition
├── database.py              # MySQL connection and logging
├── requirements.txt
└── screenshots/


Setup & Run

Prerequisites


Python 3.8+
MySQL server running locally
A working microphone (for voice mode)


1. Install dependencies

bashpip install -r requirements.txt

requirements.txt

SpeechRecognition
googletrans==4.0.0rc1
mysql-connector-python
pyaudio


Note: pyaudio may require additional system packages. On Ubuntu: sudo apt-get install portaudio19-dev. On Windows, install the matching wheel from here.



2. Set up the database

Run the following SQL to create the logging table:

sqlCREATE DATABASE translator_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

USE translator_db;

CREATE TABLE translations (
    id INT AUTO_INCREMENT PRIMARY KEY,
    source_language VARCHAR(50),
    target_language VARCHAR(50),
    input_text TEXT CHARACTER SET utf8mb4,
    output_text TEXT CHARACTER SET utf8mb4,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);


The utf8mb4 charset is required for full Unicode support including Urdu, Arabic, and emoji.



3. Configure database credentials

Update database.py with your MySQL credentials:

pythonDB_CONFIG = {
    'host': 'localhost',
    'user': 'your_user',
    'password': 'your_password',
    'database': 'translator_db',
    'charset': 'utf8mb4'
}

4. Run

bashpython main.py


How It Works

Voice mode

Microphone input
    → SpeechRecognition captures audio
    → Google Speech Recognition API transcribes
    → Detected text passed to Googletrans
    → Translation displayed in output panel
    → Both input + output logged to MySQL

Text mode

Typed input
    → Googletrans translates
    → Output displayed
    → Logged to MySQL


Testing

The application was validated using three testing approaches:


Regression testing — re-running previously passing translation cases after each code change to catch regressions
Random testing — passing varied, unexpected inputs (mixed scripts, empty strings, punctuation-only) to find edge cases
Oracle-based testing — comparing output against a known-correct reference (manual translation or an independent tool) to verify accuracy



University: COMSATS University Islamabad, Wah Campus
