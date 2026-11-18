<div align="center">

# 🎓 University Assistant

### A bilingual (Arabic 🇪🇬 / English 🇬🇧) chatbot for Innovation University (IU) students

![Python](https://img.shields.io/badge/Python-3.8+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Tkinter](https://img.shields.io/badge/GUI-Tkinter-17365D?style=for-the-badge)
![scikit-learn](https://img.shields.io/badge/ML-scikit--learn-F7931E?style=for-the-badge&logo=scikitlearn&logoColor=white)
![Languages](https://img.shields.io/badge/Languages-AR%20%7C%20EN-16804A?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-blue?style=for-the-badge)

*Ask about working hours, exams, departments, LMS, SIS and more, in Arabic (including Egyptian dialect) or English.*

</div>

---

## 📑 Table of Contents

- [About](#-about)
- [Features](#-features)
- [Screenshots](#-screenshots)
- [How It Works](#-how-it-works)
- [Supported Topics](#-supported-topics)
- [Installation](#-installation)
- [Usage](#-usage)
- [Project Structure](#-project-structure)
- [Customization](#-customization)
- [Future Improvements](#-future-improvements)
- [Contributing](#-contributing)
- [License](#-license)

---

## 📖 About

**University Assistant** is a desktop chatbot built with Python that helps students of **Innovation University (IU)** get quick answers to common questions and fast access to important university links.

It combines **rule-based keyword matching** with a **machine learning classifier** (TF-IDF + Logistic Regression), so it can answer both exact questions and loosely-phrased ones, in **Arabic and English**.

---

## ✨ Features

| | Feature | Description |
|---|---|---|
| 🌍 | **Bilingual** | Automatically detects Arabic or English and replies in the same language |
| 🧠 | **Hybrid AI** | Keyword matching first, ML prediction as a smart fallback |
| 🔤 | **Arabic normalization** | Handles letter variants (أ/إ/آ → ا, ة → ه, ى → ي) for better matching |
| 🔐 | **Student login screen** | Name and Student ID validation before chatting |
| ⚡ | **Quick-question buttons** | One-click access to Working Hours, Departments, Exams, LMS, SIS, Student Hub |
| 💬 | **Clean chat UI** | Scrollable chat with colored sender labels |
| 🛡️ | **Confidence threshold** | Replies "I don't understand" instead of guessing when confidence is below 30% |
| 🧹 | **Clear chat & logout** | Reset the conversation or switch student easily |

---

## 🖼️ Screenshots

> 📌 Add your screenshots to a `screenshots/` folder and update the paths below.

| Login Screen | Chat Window |
|:---:|:---:|
| ![Login](screenshots/login.png) | ![Chat](screenshots/chat.png) |

---

## 🧩 How It Works

```
 User message
      │
      ▼
 ┌───────────────────┐
 │ Normalize text    │  lowercase, trim, unify Arabic letters
 └─────────┬─────────┘
           ▼
 ┌───────────────────┐   match found
 │ Keyword matching  │ ───────────────► Return response
 └─────────┬─────────┘
           │ no match
           ▼
 ┌───────────────────┐
 │ TF-IDF vectorizer │  unigrams + bigrams
 └─────────┬─────────┘
           ▼
 ┌───────────────────┐   confidence ≥ 0.30
 │ Logistic Regression│ ──────────────► Return predicted response
 └─────────┬─────────┘
           │ confidence < 0.30
           ▼
   "Sorry, I don't understand."
```

1. **Language detection** uses a Unicode range check for Arabic characters.
2. **Keyword matching** gives fast, precise answers for known phrases.
3. **ML fallback** (`TfidfVectorizer` + `LogisticRegression`) classifies the intent of unseen phrasing.
4. **Confidence threshold** avoids wrong answers when the model is unsure.

---

## 🗂️ Supported Topics

| Intent | Example questions (EN / AR) |
|---|---|
| 👋 Greeting | `hello`, `hi` / `مرحبا`, `السلام عليكم` |
| 🕘 Working hours | `working hours` / `مواعيد العمل`, `الجامعة بتفتح الساعة كام` |
| 🏛️ Departments | `departments` / `اقسام الجامعة`, `التخصصات` |
| 📝 Exams | `exam schedule` / `جدول الامتحانات` |
| 🧑‍🎓 Student Affairs | `student affairs` / `شؤون الطلاب` |
| 🏫 University info | `about university` / `معلومات عن الجامعة` |
| 💻 Computer Science | `cs department` / `علوم الحاسب` |
| 📚 LMS | `lms`, `learning platform` / `منصة التعليم` |
| 🗄️ SIS | `sis`, `student information system` / `نظام الطلاب` |
| 📧 Student email | `student email` / `البريد الالكتروني` |
| 🤝 Student Hub | `student hub` / `ستودنت هب` |

---

## 🚀 Installation

### Prerequisites

- **Python 3.8+**
- `tkinter` (included with most Python installations)

> 💡 On Linux, if Tkinter is missing: `sudo apt install python3-tk`

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install scikit-learn
```

---

## ▶️ Usage

```bash
python main.py
```

1. Enter your **name** and **numeric Student ID** on the login screen.
2. Type a question in Arabic or English, or tap a **Quick Question** button.
3. Use **CLEAR CHAT** to reset the conversation, or **LOGOUT** to return to the login screen.

**Example conversation**

```
You: working hours
Assistant: University working hours are from 9 AM to 4 PM. Please verify official hours.

أنت: ايه الاقسام
المساعد: الجامعة بها أقسام أكاديمية مختلفة. تواصل مع شؤون الطلاب لمعرفة الأقسام المتاحة.
```

---

## 📁 Project Structure

```
📦 university-assistant
 ┣ 📜 main.py          # Application (data, model, logic, GUI)
 ┣ 📂 screenshots/     # Images used in this README
 ┣ 📜 requirements.txt # Dependencies
 ┗ 📜 README.md
```

`requirements.txt`:

```
scikit-learn
```

---

## 🛠️ Customization

### Add a new topic

**1.** Add training examples and labels:

```python
training_questions += ["library", "المكتبة", "مواعيد المكتبة"]
training_labels    += ["library", "library", "library"]
```

**2.** Add keywords in `get_response()`:

```python
"library": ["library", "المكتبة"],
```

**3.** Add the response (Arabic first, English second):

```python
"library": (
    "المكتبة مفتوحة من 9 إلى 4.",
    "The library is open from 9 AM to 4 PM."
),
```

### Tune the confidence threshold

```python
if confidence < 0.30:   # raise for stricter answers, lower for more lenient
```

---

## 🔮 Future Improvements

- [ ] Move training data and responses to a JSON/CSV file
- [ ] Add more intents (fees, registration, library, transportation)
- [ ] Save chat history per student
- [ ] Dark mode
- [ ] Package as an executable (`.exe`) with PyInstaller
- [ ] Web version (Flask / FastAPI)

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the project
2. Create your branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m "Add amazing feature"`
4. Push: `git push origin feature/amazing-feature`
5. Open a Pull Request

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for more information.

---

<div align="center">

Made with ❤️ for **Innovation University (IU)** students

⭐ If you like this project, give it a star!

</div>
