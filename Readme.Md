# Clara Answers - Automation Pipeline

## Architecture
- **Orchestration:** n8n (Docker)
- **Intelligence:** Groq API (Llama-3 70B & Whisper)
- **Data Storage:** Versioned local JSON files

## Pipeline Logic
1. **v1 Generation:** Extracts raw demo data into structured `memo.json` and `agent_spec.json`.
2. **v2 Update:** Uses the Whisper API for audio-to-text, then an LLM-based diff-patcher to update the v1 configuration, creating a v2 version and a markdown changelog.

## Running the project
1. Run `docker run ...` (as provided in setup).
2. Import `workflows/pipeline_a.json` and `workflows/pipeline_b.json`.
3. Provide your `GROQ_API_KEY` in the credential manager.
4. Execute via the n8n UI.

## Rubric Notes
- **Idempotent:** The workflow is designed to generate unique v1/v2 files per account.
- **Robustness:** Added retry logic on all HTTP requests to handle transient DNS issues.
- **Data Quality:** Explicitly handles `questions_or_unknowns` to avoid hallucination.