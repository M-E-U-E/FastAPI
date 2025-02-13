# FastAPI
# Documentation Assistant Setup Guide

This guide will help you set up and run the Documentation Assistant project, a FastAPI-based application that processes and provides intelligent answers from markdown documentation.

## Prerequisites

- Python 3.8 or higher
- Git
- A Gemini API key
- Access to a GitHub repository containing markdown files

## Step by Step Setup

### 1. Clone and Setup Environment

```bash
# Clone the repository
git clone https://github.com/M-E-U-E/FastAPI.git
cd FastAPI

# Create virtual environment
python3 -m venv .venv

# Activate virtual environment
# On Windows:
.venv\Scripts\activate
# On macOS/Linux:
source .venv/bin/activate
```

### 2. Create Configuration Files

Create the following files in your project root:

#### .env file
```bash
touch .env
```

Add the following content to `.env`:
```
GEMINI_API_KEY=your_gemini_api_key

GITHUB_REPO_BASE=https://api.github.com/repos/username/repo
GITHUB_TOKEN=token

PINECONE_API_KEY=apikey
PINECONE_ENVIRONMENT==  # Replace with your environment
PINECONE_INDEX_NAME== # Replace with your desired index name
PINECONE_ENDPOINT=

CREWAI_DISABLE_TELEMETRY=true

ADMIN_PASSWORD_HASH= hashcode of password
```

#### .gitignore file
```bash
touch .gitignore
```

Add the following content to `.gitignore`:
```
# Virtual Environment
venv/

# Python
__pycache__/
*.pyc

# Environment Variables
.env

# Generated Files
*.json

# IDE specific files
.vscode/
.idea/
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Application

```bash
uvicorn main:app
```

The server will start at `http://127.0.0.1:8000`

### 5. Run the Gradio
```bash
python interface.py
```
## The Main Documentation of the project will be live at:
```
https://documentation-using-ai-agent.readthedocs.io/en/latest/
```

## API Usage

### Available Endpoints

1. **Fetch Documentation**
   ```bash
   GET /fetch_docs
   ```
   Fetches and processes markdown files from the configured GitHub repository.

2. **Ask Questions**
   ```bash
   POST /ask_doc_assistant
   ```
   ```json
   {
     "query": "Your question here",
     "user_context": "Context about your question"
   }
   ```

3. **View Documentation Content**
   ```bash
   GET /docs_content
   ```
   Returns the processed documentation content.

4. **Save Documentation**
   ```bash
   GET /save_docs
   ```
   Saves the documentation to JSON files.

### Example API Calls

```bash
# Fetch documentation
curl http://localhost:8000/fetch_docs

# Ask a question
curl -X POST http://localhost:8000/ask_doc_assistant \
  -H "Content-Type: application/json" \
  -d '{"query": "How do I start?", "user_context": "New user"}'
```

## Project Structure

```
documentation-assistant/
├── venv/
├── main.py
├── requirements.txt
├── .env
├── .gitignore
└── README.md
```

## Troubleshooting

### Common Issues and Solutions

1. **Module Import Errors**
   ```bash
   pip install --upgrade -r requirements.txt
   ```

2. **Environment Variables Not Loading**
   - Verify .env file location
   - Check python-dotenv installation
   ```bash
   pip install python-dotenv
   ```

3. **API Call Failures**
   - Verify API keys in .env
   - Check GitHub repository URL
   - Test internet connection

4. **Server Start Issues**
   - Check if port 8000 is available
   - Try alternate port:
   ```bash
   uvicorn main:app --reload --port 8001
   ```

## Notes
- Implement CrewAI
  

- Keep your API keys secure and never commit them to version control
- The application processes markdown files only
- Large repositories may take longer to process
- Vector search is used for efficient document retrieval

## Additional Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Gemini API Documentation](https://cloud.google.com/vertex-ai/docs/generative-ai/model-reference/gemini)
- [FAISS Documentation](https://github.com/facebookresearch/faiss/wiki)

## Support

If you encounter any issues or need assistance:
1. Check the troubleshooting section
2. Review the API documentation at `/docs`
3. Submit an issue in the repository

Remember to update your dependencies regularly and keep your API keys secure.
