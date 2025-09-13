Q&A Bot PoC (RAG) - Project
===========================

This PoC demonstrates a Retrieval-Augmented Generation pipeline for a large PDF manual.
It includes scripts to preprocess a PDF into text chunks, build a FAISS index with embeddings,
and a FastAPI app with a single /ask endpoint that retrieves context and (optionally) calls an LLM.

Structure:
- requirements.txt
- app/            -> FastAPI server code (app.py, utils.py)
- scripts/        -> preprocess.py, build_index.py
- data/           -> store extracted chunks, index, and sample files
- sample_manual.txt -> small sample manual text for testing

Notes:
- This is a PoC. For production, add authentication, robust error handling, monitoring,
  and consider hosted vector DBs (Pinecone/Weaviate) for scale.
- You will need an API key for OpenAI if you enable LLM responses. Place it in OPENAI_API_KEY env var.

Run (quickstart):
1. Create and activate virtual environment.
2. pip install -r requirements.txt
3. Place your manual PDF at data/manual.pdf (or use sample_manual.txt included).
4. python3 scripts/preprocess.py --input data/manual.pdf --out data/chunks.json
5. python3 scripts/build_index.py --chunks data/chunks.json --out data/faiss_index
6. Start server: uvicorn app.app:app --reload --port 8001
7. Ask: GET http://127.0.0.1:8001/ask?query=your+question
