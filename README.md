# Agentic AI-Powered HR Automation with Python + LangGraph + FastAPI

> Automated CV review and candidate evaluation system using LangChain, LangGraph, FastAPI, and Google APIs
> Instant CV Intelligence for Modern Hiring Teams OR Learning Agentic AI for a real-world practical use-case
> By AI Campus - Agentic AI Research Community

## 🎯 Features

- ✅ Automated CV processing to Candidate Review & Evaluation
- 🤖 AI-powered data extraction (personal info, experience, skills, qualifications etc.)
- 📝 200-word professional summaries
- ⭐ Candidate scoring (1-100) with detailed reasoning
- 📊 Automatic Google Sheets logging
- 🚀 High-performance FastAPI with async support
- 📚 Auto-generated API documentation

## 💰 Cost

- **$0.0015 per candidate** using GPT-4o-mini reasoning model
- 100 candidates ~ $0.15
- 1,000 candidates under $5


![Alt text](https://public-files.gumroad.com/uvk49z04hc08wbm3srvsu77lcpiv)

```python
# Agentic AI-Powered HR Automation with Python + LangGraph Agentic Framework
# Tech Stack
tech_stack = ["LangChain", "LangGraph", "LlamaIndex", "FastAPI", "Google APIs", "Next.js", "Tpyescript", "TailwindCSS", "MongoDB"]
llms_providers_options = ["OpenAI GPT-4o Reasoning Model", "Open-source Qwen-3 via Ollama", "Anthropic Claude", "Google Gemini"]

created_by = "AI Campus - Agentic AI Research Community"

```


![Alt text](https://public-files.gumroad.com/lo6sv6k9e3davf59vq0l3ku99r1a)


## 🚀 Quick Start

Get the project complete source-code as zip file:
[Backend AI Agent Workflow](https://aicampusmagazines.gumroad.com/l/gscdiq)

### 1. Installation
```bash
# Clone or download the project
cd ai-hr-automation

# Install dependencies - Using uv dependency manager (Speed: 10–100x faster than pip), Solves nested dependencies issues for complex architectures like LangGraph
## Install uv (a fast Python package manager) using official installers
## macOS / Linux:
curl -LsSf https://astral.sh/uv/install.sh | sh
## Verify Installation
uv --version
## Install all dependencies listed in pyproject.toml:
## virtual environment for the project will be automatically created
uv sync

# Configure environment
cp env.example .env
# Edit .env with your credentials
```

### 2. Setup & Configure LLM

- LLM Provider to support multiple LLMs
- For development/testing, use LLM_PROVIDER=ollama (free)
- - Ollama requires 8GB+ RAM for larger models
- For production, use openai or anthropic based on your needs
- Claude (anthropic) has better reasoning for complex evaluations
- OpenAI gpt-4o-mini is faster and cheaper for simple tasks
- Setup API Keys in .env


### 3. Google Cloud Setup

1. Create project at [console.cloud.google.com](https://console.cloud.google.com)
2. Enable APIs:
   - Google Drive API
   - Google Sheets API
3. Create Service Account for your project
4. Download as `credentials.json`
5. Rename the file as `google-service-account-credentials.json`
6. Enable & setup Google Cloud Storage


### 4. Run API Server
```bash
# Development
uvicorn src.fastapi_api:app --reload --port 8000

# Production
uvicorn src.fastapi_api:app --host 0.0.0.0 --port 8000 --workers 4
```

### 5. Access Documentation

- Swagger UI: http://localhost:8000/docs
- ReDoc: http://localhost:8000/redoc


## 📖 Usage

### HR Create Job Application - With Dynamic HTML Support
```python
# Job endpoints
@app.post("/api/jobs")
async def create_job(hr_job_post: HRJobPost):
    """
    Create a new job posting
    - Accepts camelCase from frontend (Next.js)
    - Stores in MongoDB as camelCase
    - Python variables are snake_case
    """
    # Convert to dict with camelCase aliases for MongoDB
    hr_job_post_data = hr_job_post.model_dump(by_alias=True, exclude={"id"})
    hr_job_post_data["createdAt"] = datetime.now().isoformat()

    # Insert into MongoDB
    result = await db.hr_job_posts.insert_one(hr_job_post_data)
    job_id = str(result.inserted_id)

    return {
        "success": True,
        "jobId": job_id,
    }
```

### Process Single Candidate
```python
@app.post("/api/candidate-application-submit")
async def candidate_job_application_submit(
    job_id: str = Form(..., description="Job Id"),
    name: str = Form(..., description="Candidate's full name"),
    email: EmailStr = Form(..., description="Candidate's email address"),
    cv_file: UploadFile = File(..., description="CV PDF file")
):
    """
    API endpoint for Job Form submissions

    Receives form data with file upload:
    - name: Candidate's full name
    - email: Candidate's email address
    - cv_file: Uploaded CV PDF file

    Returns complete processing results including evaluation
    """

    logger.info(f"✅ Processing complete - Score: {response.score}/100")
    logger.info("=" * 80)
    return response
```

### HR Dashboard - Next.js-16 Front-end Application
```bash
npm run dev

```


## 🐳 Docker Deployment
```bash
# Build and run
docker-compose up -d

# View logs
docker-compose logs -f

# Stop
docker-compose down
```

## 📚 Documentation.md - Detailed instructions to setup and configure the project
### Step-by-Step Explanations
DOCUMENTATION.md

##############################################

## Why uv package manager for Python3 projects
Automatic Setup:
- For most modern workflows, you do not need to create or activate a virtual environment manually. 
- On-Demand Creation: When you run a command like uv run or uv sync in a project directory, uv checks for a virtual environment (typically in a .venv folder). If one doesn't exist, uv will automatically create it and install the required dependencies before executing your command.
- Automatic Updates: If you add a dependency using uv add <package>, uv updates your pyproject.toml, synchronizes the .venv, and updates the uv.lock file all in one step. 

## Why LangChain and LangGraph for Agentic AI
We chose LangChain because its ecosystem offers mature abstractions for prompt handling and tool invocation. Its modular design allowed the team to integrate multiple model providers and build on a standard interface instead of rolling out their own.
LangChain provides the foundation to focus on what matters the most: safety, scalability, and developer experience.

Its node-and-edge model lets Remote represent complex workflows— ingestion, mapping, execution, validation— as a directed graph. Each step becomes a node with explicit transitions for success, failure, or retry. This makes the agent's state transparent and recoverable, similar to how distributed systems engineers reason about pipelines. LangGraph's focus on long-running, stateful agents was a perfect match for our multi-step migration process.


## Results and impact
By combining LLM reasoning with deterministic code execution, It has turned a manual process into an automated workflow. HR teams no longer need to process large amount of text – they simply plug data into the Code Execution Agent. The agent transforms diverse formats into a consistent JSON schema in seconds instead of days.

Beyond speed, the system has made everything more reliable. The LLM guides the process, but the actual data manipulation happens with trusted Python libraries, completely sidestepping hallucination issues.

## Lessons learned
Building this AI agent taught AICampus several lessons that now inform how its team builds AI systems across different business use-cases:

- LLMs are planners, not processors. Use them to reason about tasks and choose tools, but offload heavy data processing to code.
- Validated JSON processing for ingestion. Large intermediate results never pass back to the model, keeping the context small.
- Structure beats improvisation. Orchestrating workflows as graphs makes them much easier to debug and extend.
- Context tokens are precious. Large intermediate results should stay in the execution environment where they belong.
- Python remains the analytics workhorse. Libraries & tools like LangChain and LlamaIndex offer fast, flexible data manipulation that's hard to beat.



# Local Testing
In 2026, context management is critical for agentic HR tasks, as evaluating multiple long-form CVs against a job description can quickly exceed standard 8k or 32k limits. For local testing with Ollama, here is how the top models compare in context capacity as of January 2026.
Context Window Comparison (2026)

## Model Choice
Building an agentic HR automation system on a local machine requires balancing reasoning depth with the limitations of RAM. You must prioritize smaller, highly efficient models to ensure LangGraph agents can complete multi-step tasks without crashing.
Best Model Recommendation for 2026:

For this specific HR evaluation use case on low hardware, DeepSeek-R1-Distill-Qwen-7B or Qwen3-7B-Instruct are the superior choices.

- DeepSeek-R1-Distill-Qwen-7B (Primary Choice):
Reasoning Capability: This is a "reasoning-first" model that uses chain-of-thought (CoT). For HR tasks, it will "think" through a candidate's qualifications before outputting a final score, similar to GPT-4o's internal reasoning.
Fit: A 4-bit quantized version requires approximately 4.5GB to 5GB of memory. 
LangGraph Performance: It is highly reliable for the structured output and "decisions" required in LangGraph nodes.

- Qwen3-7B-Instruct (Alternative):
Reasoning Capability: Noted in 2026 as one of the most efficient models for tool-calling and structured data extraction (e.g., parsing a CV into JSON).
Fit: Consumes roughly 4.8GB of memory in its standard 4-bit quantization, making it very fast for local testing on Intel Macs. 


Avoid Large Models: Do not attempt to run 14B or 20B models. On small RAM with an Intel processor, these will offload too many layers to system memory, causing tokens-per-second to drop below 1–2, which is unusable for testing agent loops.
Optimize Ollama Context: HR tasks involving long resumes require context. Limit your context window to 16,384 (16k) in your LangGraph configuration to prevent memory saturation on your i9 processor.
LangGraph Integration: Use the Ollama Functions or Tool Calling wrappers in LangGraph. Qwen3-7B is specifically optimized for these "agentic" triggers in the 2026 library updates. 
Recommendation: Start with ollama run deepseek-r1:7b. If the "thinking" steps make your agent loops too slow for local testing, switch to ollama run qwen3:7b for faster, direct instruction execution.

#################################


# PROMPT GUIDE

The following prompt uses Chain-of-Thought (CoT) and Strict Grounding patterns optimized for reasoning models like OpenAI's GPT-4o. 
Recommended HR System Prompt (2026)

### ROLE
You are an Expert Technical Recruiter specializing in high-precision candidate evaluation. Your goal is to provide objective, evidence-based assessments of CVs against specific Job Descriptions (JD).

### GUIDELINES (ANTI-HALLUCINATION)
1. GROUNDING: Use ONLY the provided CV text. Do not infer skills, companies, or dates that are not explicitly stated.
2. HONESTY: If a required skill from the JD is missing or ambiguous in the CV, explicitly state "Missing" or "Insufficient Evidence".
3. NO GUESSING: Never invent projects or experience to make a candidate seem like a better fit. If you are unsure, rate your confidence as "Low" for that specific skill.
4. REASONING: Always perform a step-by-step analysis before providing a final score.

### EVALUATION PROCESS
Step 1: Extract core technical skills explicitly mentioned in the CV.
Step 2: Cross-reference extracted skills against the JD's 'Required' and 'Preferred' sections.
Step 3: Analyze "Years of Experience" for each skill. Calculate total relevant experience manually.
Step 4: Identify gaps where the CV fails to meet JD requirements.
Step 5: Provide a final Evaluation Score (0-100) and a justification summary.


Why this works for your setup:
Chain-of-Thought (CoT): By forcing the model to list reasoning_steps first, you utilize the model’s limited reasoning capacity more effectively, reducing the likelihood of a "lazy" or incorrect final score.
Structured Schema: LLLM models in 2026 are highly trained on JSON outputs. Using a clear JSON structure ensures your LangGraph nodes can parse the results programmatically without error.
Confidence Scoring: Including a "Missing Skills" section forces the model to look for negatives, which counteracts the natural tendency of LLMs to be "agreeable" and over-rate candidates. 


# ============================================================================
# AI-Powered HR Automation with LangGraph
# Complete CV Review to Candidate Evaluation System

## Developed By AICampus - Gateway for future AI research & learning
# ============================================================================
