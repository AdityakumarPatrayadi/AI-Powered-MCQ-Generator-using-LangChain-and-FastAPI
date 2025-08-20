# AI-Powered-MCQ-Generator-using-LangChain-and-FastAPI

This project is a robust web service that automatically generates Multiple Choice Questions (MCQs) from a given piece of text. It leverages the power of Large Language Models (LLMs) through the LangChain framework and serves the functionality via a high-performance FastAPI backend.

This tool is ideal for educators, content creators, and students who need to quickly create quizzes and assessments from articles, documents, or any other text-based content.

## ✨ Features

-   **Automated MCQ Generation**: Instantly create MCQs from any provided text.
-   **Customizable Requests**: Specify the number of questions, the subject/topic, and the complexity/tone.
-   **Structured JSON Output**: The API returns well-formatted JSON, making it easy to integrate with other applications.
-   **High-Performance Backend**: Built with FastAPI for fast, asynchronous request handling.
-   **Scalable AI Logic**: Uses LangChain to orchestrate prompts and interactions with LLMs, making it easy to swap models or modify logic.

## 🛠️ Tech Stack & Architecture

The project follows a simple yet powerful architecture to process requests and generate MCQs.

**Workflow:**
`User Request -> FastAPI Endpoint -> LangChain Chain -> Formatted Prompt -> LLM (OpenAI/Google) -> Output Parser -> JSON Response -> User`

**Key Technologies:**
-   **Backend**: [FastAPI](https://fastapi.tiangolo.com/)
-   **AI Orchestration**: [LangChain](https://www.langchain.com/)
-   **Language Models**: [OpenAI GPT series](https://openai.com/), [Google Gemini](https://deepmind.google/technologies/gemini/), or other compatible LLMs.
-   **Environment Management**: [python-dotenv](https://pypi.org/project/python-dotenv/)
-   **Server**: [Uvicorn](https://www.uvicorn.org/)

---

## ⚙️ Setup and Installation

Follow these steps to get the project running on your local machine.

### 1. Clone the Repository

```bash
git clone https://github.com/krishnaik06/MCPSERVERLangchain.git
cd MCPSERVERLangchain
```

### 2. Create and Activate a Virtual Environment

It's highly recommended to use a virtual environment to manage project dependencies.

-   **For macOS/Linux:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    ```
-   **For Windows:**
    ```bash
    python -m venv venv
    .\venv\Scripts\activate
    ```

### 3. Install Dependencies

Install all the required Python libraries using the `requirements.txt` file.

```bash
pip install -r requirements.txt
```

### 4. Set Up Environment Variables

The project requires API keys for the LLM service you intend to use.

-   Create a new file named `.env` in the root of the project directory.
-   Copy the contents of `.env.example` (if it exists) or add the following keys to your new `.env` file:

    ```env
    # Choose the LLM provider you want to use and add the corresponding API key
    
    # For OpenAI
    OPENAI_API_KEY="sk-..."
    
    # For Google Gemini
    GOOGLE_API_KEY="..."
    ```

    **Note:** You only need to provide the key for the service you have configured in the source code.

---

## ▶️ How to Run the Application

Once the setup is complete, you can start the web server using Uvicorn.

```bash
uvicorn main:app --reload
```

-   `main`: Refers to the `main.py` file.
-   `app`: The FastAPI instance created inside `main.py`.
-   `--reload`: This flag automatically restarts the server whenever you make changes to the code.

The server will be running at `http://127.0.0.1:8000`.

## 📚 API Usage

You can interact with the API using the interactive documentation provided by FastAPI or by sending requests using tools like `curl` or Postman.

-   **Interactive Docs (Swagger UI)**: Navigate to `http://127.0.0.1:8000/docs` in your browser.

### Endpoint: `POST /mcq-generator`

This endpoint generates the MCQs.

**Request Body:**
You need to send a JSON object with the following fields:

```json
{
  "text": "Your long piece of text goes here. For example, a paragraph about photosynthesis...",
  "number": 5,
  "subject": "Biology",
  "tone": "simple"
}
```

**Example `curl` Request:**

```bash
curl -X 'POST' \
  'http://127.0.0.1:8000/mcq-generator' \
  -H 'Content-Type: application/json' \
  -d '{
    "text": "Photosynthesis is a process used by plants, algae, and certain bacteria to convert light energy into chemical energy, through a process that converts carbon dioxide and water into sugars and oxygen.",
    "number": 2,
    "subject": "Biology",
    "tone": "simple"
  }'
```

**Example Success Response (200 OK):**

The API will return a JSON object containing the generated quiz.

```json
{
  "quiz": {
    "1": {
      "mcq": "What is the primary purpose of photosynthesis?",
      "options": {
        "a": "To consume oxygen",
        "b": "To convert light energy into chemical energy",
        "c": "To produce carbon dioxide",
        "d": "To absorb water from the soil"
      },
      "correct": "b"
    },
    "2": {
      "mcq": "What are the main inputs for photosynthesis?",
      "options": {
        "a": "Sugars and oxygen",
        "b": "Light energy and water",
        "c": "Carbon dioxide and water",
        "d": "Chemical energy and sugars"
      },
      "correct": "c"
    }
  }
}

## 📂 Project Structure


.
├── .github/                # GitHub Actions workflows
├── mcqgenerator/           # Main source code package
│   ├── __init__.py
│   ├── logger.py           # Logging configuration
│   ├── mcqgenerator.py     # Core LangChain logic for the MCQ chain
│   └── utils.py            # Utility functions
├── .env                    # Environment variables (API keys)
├── main.py                 # FastAPI application entry point
├── requirements.txt        # Project dependencies
├── setup.py                # Package setup script
└── test.py                 # Test script for the application

