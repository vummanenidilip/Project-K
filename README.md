# Project-K
Langgraph-ResumePrototype
# AI-Powered Resume-to-Job Matcher & Career Coach (Prototype)

## Project Overview

This project is an AI-powered prototype designed to assist job seekers by intelligently matching their resume skills with job description requirements and providing personalized interview preparation advice. It leverages Large Language Models (LLMs) and LangGraph to create a structured and actionable workflow.

## Features

* **PDF Text Extraction**: Extracts raw text from both resume PDF and job description PDF files.
* **Intelligent Skill Matching**: Uses an LLM (GPT-4o) to:
    * Identify key technical and soft skills from both the resume summary and the job description.
    * Compare these skills to determine the resume's suitability for the job.
    * Provide a concise reason for the match decision.
    * Highlight specific skills from the job description that are missing or need strengthening in the resume.
* **Personalized Career Coaching**: A dedicated "guider" tool suggests 3-5 crucial technical topics for the candidate to review based on the skill gap analysis.
* **Modular Workflow**: Built with LangGraph for a clear, extensible, and stateful multi-step process.

## How It Works

The system operates as a sequential graph with two main nodes:

1.  **LLM Node (`llm` tool)**:
    * **Input**: Takes `resume_summary` (text content of the resume) and `job_description` (text content of the job description) as direct string inputs.
    * **Process**: Utilizes `gpt-4o` with a carefully crafted prompt to perform skill extraction and compatibility analysis.
    * **Output**: Returns a JSON object containing:
        * `extracted_resume_skills`
        * `extracted_jd_skills`
        * `analysis` (list of skills to prepare)
        * `match_result` ("Suitable" or "Not Suitable")
        * `reason` for the match result.

2.  **Guider Node (`guider` tool)**:
    * **Input**: Receives the `analysis` output (list of skills to prepare) from the LLM Node.
    * **Process**: Acts as a career coach, using a prompt to interpret the skill gaps.
    * **Output**: Provides practical advice on 3-5 technical topics the candidate should brush up on for the interview.

**Workflow Flow:**
`LLM NODE` (Entry Point) --> `GUIDER NODE` (Finish Point)

## Setup and Installation

### Prerequisites

* Python 3.8+
* `pip` package manager
* OpenAI API Key
* Hugging Face API Key (if you plan to extend with Hugging Face models)

### Steps

1.  **Clone the repository:**
    ```bash
    git clone <your-repository-url>
    cd <your-repository-name>
    ```

2.  **Create a virtual environment (recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
    * **Note**: You'll need to create a `requirements.txt` file. Based on your `code.ipynb`, it should include:
        ```
        pypdf
        python-dotenv
        langchain
        langchain-openai
        langgraph
        ```

4.  **Set up Environment Variables:**
    Create a `.env` file in the root directory of your project and add your API keys:
    ```env
    OPENAI_API_KEY="your_openai_api_key_here"
    ```
    *Ensure
