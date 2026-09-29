# DecisionOS

## Problem
People often make important decisions using information that is fragmented, incomplete, contradictory, and difficult to compare. The internet contains much of the required information, but users must manually perform the investigation across dozens of tabs, synthesizing conflicts and identifying what they missed.

## Why This Problem Matters
Decisions like evaluating a job offer, buying a property, or purchasing a used vehicle have massive personal and financial consequences. Making these decisions blindly due to research fatigue leads to sub-optimal outcomes. 

## Solution
DecisionOS is an AI due-diligence and decision-intelligence agent that turns ambiguous real-world decisions into evidence-backed action plans. 
"Don't just search. Investigate."

## Product Workflow
1. **User Goal**: The user provides the decision they are trying to make.
2. **Research Plan**: The agent converts the context into a prioritized list of specific research questions.
3. **Live Search**: The agent routes questions to appropriate SerpApi engines.
4. **Evidence Extraction**: The agent extracts verifiable claims tied directly to source URLs.
5. **Gap Detection**: The agent analyzes what is *missing* from the extracted evidence.
6. **Action Plan**: The agent synthesizes the evidence and gaps into a structured dossier with next actions.

## Key Features
*   **Decision-aware Research Planning**: Dynamically generates queries based on the decision type.
*   **Dynamic SerpApi Engine Selection**: Routes searches to Google Organic, Google News, or Google Jobs as appropriate.
*   **"What Am I Missing?" Gap Detection**: Automatically highlights critical unknowns before you make a decision.
*   **Evidence-First UI**: Claims are tied to verifiable sources, reducing hallucination risks.

## Decision Packs
The MVP includes the foundational engine for:
1.  **Job Offer Due Diligence**
2.  **Property Due Diligence**
3.  **Used Vehicle Due Diligence**

## Architecture
**Frontend**: React, TypeScript, Vite, Tailwind CSS
**Backend**: Python, FastAPI, Pydantic
**Orchestration**: Custom procedural agent loop.
**Search Integration**: SerpApi (google, google_news, google_jobs)
**LLM**: Gemini / OpenAI (abstracted)

## Agent Workflow
`Goal Interpreter -> Research Planner -> Search Router -> Evidence Extractor -> Gap Detector -> Synthesizer`

## Research Loop
The system executes a bounded research loop (maximum 3 rounds for MVP) to prevent runaway agent execution while ensuring deep investigation.

## Evidence Model
All claims are extracted as structured data and assigned a confidence level and a source ID.

## Gap Detection
The Gap Detector reads the extracted claims and the original user goal to flag missing critical information, returning structured `InformationGap` objects.

## SerpApi Integration
SerpApi is fundamental to this product. A traditional LLM cannot know the latest news about a company, current job openings, or local property context. 
*   **Google Search**: Used for general company, product, and market information.
*   **Google News**: Used to detect recent developments or controversies.
*   **Google Jobs**: Used to understand current hiring context.

## Technology Stack
*   React + Tailwind CSS
*   FastAPI + Pydantic
*   SerpApi

## Project Structure
*   `frontend/`: React application.
*   `backend/`: FastAPI application and agent logic.

## Setup
1. Clone the repository.
2. Set up the environment variables.

## Environment Variables
Copy `.env.example` to `.env` and fill in:
```
SERPAPI_API_KEY=your_key
GEMINI_API_KEY=your_key
```

## Running Locally
**Backend**:
```bash
cd backend
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

**Frontend**:
```bash
cd frontend
npm install
npm run dev
```

## Example Investigation
"I received a software engineering offer from Company X for their Bengaluru office. Investigate it before I make my decision."

## Testing
API endpoints can be tested using the FastAPI Swagger UI at `http://localhost:8000/api/docs`.

## Limitations
*   The current MVP runs a single-pass research loop. True recursive gap-investigation is limited to prevent excessive API costs.
*   Data is stored in-memory and will be lost on server restart.

## Future Work
*   Persistent storage and decision history.
*   Continuous monitoring of gaps (e.g., alert me if the company is in the news).
*   Browser extension integration.

## AI Tools Used
*   Antigravity (Google DeepMind)

## Hackathon
SerpApi India Hackathon 2026
Track: AI Agents
