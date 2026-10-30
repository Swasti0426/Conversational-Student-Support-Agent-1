# Campus Companion — Student Support Agent (Assignment 1)

## 1. Overview

Campus Companion is an educational Streamlit application developed to provide AI-powered student support. It uses a Groq-hosted Large Language Model (LLM), tool functions for sample fee and scholarship records, policy lookup and retrieval, per-user chat history in SQLite, and a preference-memory module.

The application allows students to interact with an AI agent through a conversational interface to access relevant academic and administrative information.

The bundled student records are synthetic examples. No real student data should be added to the project.

## 2. Project Structure

```text
Conversational-Student-Support-Agent-1/
│
├── app.py                         # Streamlit interface and login/chat flow
├── agent.py                       # LLM orchestration and tool calling
├── tools.py                       # Fee and scholarship lookup tools
├── auth_db.py                     # SQLite authentication and conversation persistence
├── policy.py                      # Institutional policy lookup logic
├── knowledge_search.py            # Local ChromaDB knowledge retrieval
├── memory.py                      # Conversation and preference memory
├── ingest_data.py                 # Knowledge-base data ingestion and indexing
├── setup_users.py                 # Local user account setup
├── test_groq.py                   # Groq API connection testing
├── test_tools.py                  # Student-support tool testing
│
├── data/
│   ├── students.json              # Synthetic student records
│   └── student_policy.md          # Sample institutional policy text
│
├── knowledge_base/
│   ├── documents/
│   │   └── student_handbook.pdf   # Student handbook (include only if valid)
│   │
│   ├── tables/
│   │   ├── policies.csv           # Policy reference data
│   │   ├── scholarships.xlsx      # Scholarship information
│   │   └── student_fees.csv       # Student fee records
│   │
│   └── index/                     # Cached local ChromaDB retrieval index
│       ├── chroma.sqlite3
│       ├── manifest.json
│       └── [index collection folder]
│
├── evaluation/
│   ├── assignment_1_evaluation.csv # Evaluation metrics and observations
│   └── evaluation_traces.jsonl     # Sample evaluation traces (if included)
│
├── requirements.txt               # Required Python libraries
├── .env.example                   # Placeholder for Groq API key
├── .gitignore                     # Excludes sensitive and unnecessary files
└── README.md                      # Project overview and setup instructions
```

## 3. Requirements

- Windows, macOS, or Linux
- Python 3.10 or newer (Python 3.11 is recommended)
- Groq API key for LLM-powered responses
- Internet connection

## 4. Setup and Run (Windows PowerShell)

### Step 1: Clone the Repository

```powershell
git clone YOUR_GITHUB_REPOSITORY_URL
cd Conversational-Student-Support-Agent-1
```

### Step 2: Create a Virtual Environment

```powershell
python -m venv .venv
```

### Step 3: Activate the Virtual Environment

```powershell
.\.venv\Scripts\Activate.ps1
```

The terminal prompt should now begin with `(.venv)`.

If PowerShell blocks activation, run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```

Then activate the environment again.

### Step 4: Install Dependencies

```powershell
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### Step 5: Configure the Groq API Key

Create a local `.env` file by copying `.env.example` and add your own Groq API key:

```text
GROQ_API_KEY=put_your_own_key_here
```

Never upload your actual `.env` file or API key to GitHub. The `.env.example` file contains only a placeholder.

### Step 6: Create a Local Login Account

Run the account setup script:

```powershell
python setup_users.py
```

Follow the instructions to create a local student account. Use a sample student ID such as `STU1001` if it exists in `data/students.json`.

Do not use real student credentials or passwords.

### Step 7: Run the Application

```powershell
python -m streamlit run app.py
```

Open the local URL displayed in the terminal, usually:

`http://localhost:8501`

**Note:** If your project uses a different account-creation script, run the script actually included in the repository.

## 5. Key Features

- **Conversational Student Support:** Allows students to ask questions through a chat interface.
- **Fee Status Lookup:** Retrieves fee information from sample student records.
- **Scholarship Lookup:** Provides scholarship-related information.
- **Policy Retrieval:** Retrieves relevant information from institutional policy documents.
- **Knowledge Retrieval:** Uses a local ChromaDB index to retrieve relevant information.
- **Conversation History:** Maintains user-specific conversation history using SQLite.
- **Preference Memory:** Supports the preference-memory functionality implemented in the project.

## 6. Architecture at a Glance

1. **Streamlit Interface (`app.py`):** Accepts student queries through the login and chat interface.
2. **Agent Orchestration (`agent.py`):** Sends requests to the Groq-hosted language model and manages tool calls.
3. **Student Support Tools (`tools.py`):** Retrieves fee and scholarship information from synthetic student records.
4. **Policy Lookup (`policy.py`):** Supports policy-related queries.
5. **Knowledge Retrieval (`knowledge_search.py`):** Retrieves relevant information from the local ChromaDB knowledge base.
6. **Authentication and Persistence (`auth_db.py`):** Manages local account information and conversation history through SQLite.
7. **Memory (`memory.py`):** Provides preference-memory functionality.

## 7. Demo Scenarios

The following scenarios can be used to demonstrate the application:

- Ask for the logged-in sample student's current fee status.
- Ask for the logged-in sample student's scholarship status.
- Ask a question about an institutional policy included in the knowledge base.
- Ask a follow-up question to test conversational context.
- Refresh the application and verify whether the conversation history persists.

## 8. Evaluation

The Student Support Agent was evaluated using 14 recorded interaction traces.

### Evaluation Metrics

| Evaluation Metric | Result |
|---|---:|
| Number of Evaluation Traces | 14 |
| Average Latency | 1.811 seconds |
| Average Input Tokens | 1,106.7 |
| Average Output Tokens | 74.9 |

### Key Observations

- Fee status lookup was tested using sample student records.
- Scholarship lookup was tested.
- Policy retrieval returned relevant information.
- Conversation context was tested through follow-up questions.
- Student data privacy was tested through a cross-student query.

These results represent observations from the supplied evaluation sample. They are descriptive measurements, not a controlled benchmark or a formal overall accuracy score.

Detailed evaluation results and supporting traces are provided in the `evaluation/` folder, where included.

## 9. Demonstration Video

The project demonstration video explains the application workflow, architecture, student-support tools, knowledge retrieval, conversation memory, and evaluation.

**Video Link:** [Insert your Google Drive or YouTube video link here]

## 10. Security and Privacy Notes

- Never commit `.env` files, API keys, passwords, tokens, local databases, chat logs, or personal data.
- The public repository should exclude runtime SQLite databases and personal conversation-memory files.
- Sample student records are fictional examples.
- Do not use real student information.
- This project is an educational prototype, not a production-ready student information system.
- Authentication, authorization, privacy, logging, and deployment controls require further review before real-world use.

## 11. Known Limitations

- The language model requires a valid Groq API key and an active internet connection.
- Policy answer quality depends on the available policy Markdown/CSV files and the knowledge-base index.
- The cached ChromaDB index may need to be rebuilt or validated if knowledge-base documents or tables are changed.
- The availability of handbook-based retrieval depends on the presence of a valid handbook PDF.
- Some supplied evaluation cases are partial or require further retesting.
- The limited evaluation sample does not establish production-level reliability or perfect accuracy.

## 12. Conclusion

Campus Companion demonstrates the implementation of an AI-powered student-support agent using conversational AI, tool calling, knowledge retrieval, and preference memory.

The project provides a practical example of how Agentic AI can simplify common student-support activities and improve access to institutional information.

## 13. Before Public GitHub Submission

- Confirm that `.env` and actual API keys are excluded.
- Confirm that no real credentials or student information are committed.
- Exclude local databases, private chat histories, and unnecessary virtual-environment files.
- Verify that all files mentioned in the README are present.
- Test the setup using a fresh virtual environment.
- Make the repository public if required by the assignment.
- Verify that the repository link works in a private/incognito browser.
