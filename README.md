# AI Call Auditor

**AI Call Auditor** is a comprehensive tool designed to automate the quality assurance process for customer support interactions. Leveraging advanced Generative AI and Retrieval-Augmented Generation (RAG), it audits audio calls and chat logs against company policies, providing detailed insights, scoring, and compliance reports.

## 🚀 Features

-   **Multi-Format Support**: Upload and analyze both audio files (`.mp3`, `.wav`) and chat logs (`.txt`, `.json`).
-   **Automated Transcription & Diarization**: Uses **OpenAI Whisper** for high-accuracy transcription and **Senko** for speaker diarization (processed on CPU/GPU).
-   **Policy-Aware Auditing (RAG)**: Dynamically retrieves relevant company policies using RAG (LangChain + FAISS) to ensure audits are contextually accurate.
-   **llm-Powered Analysis**: Utilizes **Google Gemini (gemini-3-flash-preview)** to evaluate interactions for empathy, professionalism, clarity, resolution, and compliance.
-   **Automated Reporting**: Generates detailed **PDF Reports** for every audit.
-   **Critical Alerts**: Automatically sends email notifications to managers for interactions with low scores (< 30).
-   **Audit History**: Stores all audit logs in a local **SQLite** database for historical tracking.
-   **Policy Management**: View and manage the active company policy directly from the UI.

## 📂 Project Structure

```
AI-Call-Auditor/
├── app.py                  # Main Streamlit application entry point
├── requirements.txt        # Python dependencies
├── .env                    # Environment variables (API Keys)
├── policies/               # Directory for policy documents
│   └── company_policy.txt  # Default policy text file
├── src/                    # Source code modules
│   ├── audio_processor.py  # Audio transcription & diarization logic
│   ├── auditor.py          # Gemini LLM interaction for auditing
│   ├── chat_normalizer.py  # Parsing logic for text/chat logs
│   ├── database_manager.py # SQLite database operations
│   ├── rag_engine.py       # RAG implementation (FAISS vector store)
│   └── reporting.py        # PDF generation and Email alerting
└── data/                   # Generated data (uploads, reports, DBs)
    ├── uploads/            # Temporary storage for uploaded files
    ├── pdf-reports/        # Generated PDF reports
    └── database/           # SQLite database file location
```

## 🛠️ Tech Stack

-   **Frontend**: Streamlit
-   **AI/LLM**: Google Gemini API, OpenAI Whisper, Senko (Diarization)
-   **RAG framework**: LangChain, FAISS (Vector Store), HuggingFace Embeddings (`all-MiniLM-L6-v2`)
-   **Backend/Utils**: Python, Pandas, SQLite
-   **Reporting**: FPDF (PDF generation), SMTP (Email)

## 📋 Prerequisites

-   **Python 3.10+** (Recommended)
-   **FFmpeg**: Required for audio processing.
    -   *Windows*: `winget install ffmpeg` or download and add to PATH.
    -   *Linux*: `sudo apt install ffmpeg`
    -   *Mac*: `brew install ffmpeg`
-   **Google Gemini API Key**: Get one from [Google AI Studio](https://aistudio.google.com/).
-   **Git**: To clone the repository.

## ⚙️ Installation

1.  **Clone the Repository**
    ```bash
    git clone <repository-url>
    cd AI-Call-Auditor
    ```

2.  **Create a Virtual Environment**
    ```bash
    python -m venv venv
    # Windows
    venv\Scripts\activate
    # Mac/Linux
    source venv/bin/activate
    ```

3.  **Install Dependencies**
    ```bash
    pip install -r requirements.txt
    ```
    *Note: This may take a few minutes as it installs PyTorch and other ML libraries.*

4.  **Configure Environment Variables**
    Create a `.env` file in the root directory and add your keys:
    ```env
    GEMINI_API_KEY=your_actual_api_key_here
    # Optional: Email configurations if you want to enable alerts
    # SENDER_EMAIL=your_email@gmail.com
    # SENDER_PASS=your_app_password
    ```

## 🚀 Usage

1.  **Start the Application**
    ```bash
    streamlit run app.py
    ```

2.  **Run an Audit**
    -   Navigate to the **Run Audit** tab.
    -   Upload an audio file or chat log.
    -   Click **Start Audit**.
    -   Wait for the 4-step process (Processing -> RAG -> Audit -> Reporting) to complete.

3.  **View Results**
    -   Results are displayed on screen with a Score and Status.
    -   Download the formal **PDF Report**.
    -   If the score is critical, an alert is simulated (or sent if email is configured).

4.  **Manage History**
    -   View past audits in the **Audit History** tab.
    -   Reset system data from the Sidebar if needed.

## 📝 Policy Customization

To audit against your specific company guidelines, simply edit the text file located at:
`policies/company_policy.txt`

The RAG engine will automatically re-index the new policy content on the next run.

## 🤝 Contributing

Contributions are welcome! Please fork the repository and submit a Pull Request.

## 📄 License

[MIT License](LICENSE)
