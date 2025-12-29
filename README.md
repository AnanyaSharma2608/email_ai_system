# Email Compliance Surveillance System

## Overview
This system provides automated email compliance monitoring using advanced language models and retrieval-augmented generation (RAG) to analyze emails against organizational policies. It helps identify potential compliance violations, mask sensitive information, and provides a dashboard for review and insights.

## Features
- **Policy Upload**: Upload and index organizational policies (PDF, DOCX, TXT formats)
- **Email Processing**: Analyze email CSV files for compliance violations
- **PII Masking**: Automatically mask personally identifiable information
- **Risk Assessment**: Assign priority levels (High, Medium, Low) to flagged emails
- **Review Interface**: Streamlit-based dashboard for reviewing and approving/rejecting flagged emails
- **Dashboard**: View compliance insights and statistics
- **API Backend**: FastAPI-based REST API for integrations

## Requirements
- Python 3.8 - 3.12 (Python 3.14 may have compatibility issues with some packages)
- OpenAI API key for LLM processing
- Required Python packages (see requirements.txt)

## Setup
1. Clone the repository
2. Create a virtual environment: `python -m venv venv`
3. Activate the virtual environment: `venv\Scripts\activate` (Windows)
4. Install dependencies: `pip install -r requirements.txt`
5. Set up environment variables in `.env` file:
   ```
   OPENAI_API_KEY=your_openai_api_key_here
   ```
6. Start the backend: `uvicorn backend.app:app --reload`
7. In a new terminal, start the frontend: `streamlit run frontend/app.py`

## Usage
1. **Upload Policies**: Use the "Upload Data" tab to upload policy documents
2. **Process Emails**: Upload a CSV file containing emails with columns: id, subject, body, attachments (optional)
3. **Review Emails**: In the "Review Emails" tab, filter and review flagged emails by priority
4. **Dashboard**: View compliance statistics and insights in the "Dashboard" tab

## API Endpoints
- `POST /upload-policies`: Upload policy files
- `POST /process-emails`: Process email CSV file
- `GET /emails`: Retrieve processed emails (with optional priority filter)
- `POST /review-email/{id}`: Approve or reject an email

## Troubleshooting
- Ensure Python version is 3.12 or earlier
- Check that OpenAI API key is correctly set in .env
- Verify all dependencies are installed
- Make sure ports 8000 (backend) and 8501 (frontend) are available
- If ChromaDB issues occur, delete the data/chroma_db folder and restart

## Project Structure
```
email-compliance-system/
├── backend/                 # FastAPI backend
│   ├── app.py              # Main API application
│   ├── models.py           # Data models
│   ├── rag.py              # RAG system for policy retrieval
│   ├── llm_pipeline.py     # LLM processing pipeline
│   ├── pii_masking.py      # PII detection and masking
│   ├── database.py         # Database operations
│   └── utils.py            # Utility functions
├── frontend/               # Streamlit frontend
│   └── app.py              # Dashboard application
├── data/                   # Data storage
│   ├── chroma_db/          # Vector database
│   ├── emails/             # Processed emails
│   └── policies/           # Policy documents
├── requirements.txt        # Python dependencies
├── README.md               # This file
└── .env                    # Environment variables
```