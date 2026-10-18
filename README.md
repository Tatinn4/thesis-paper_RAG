# thesis-rag

My first RAG project. It loads a research paper (PDF), cleans and chunks the text, embeds the chunks with BAAI/bge-small-en-v1.5, and searches them with a FAISS index.

Put your own PDF in a `papers/` folder, then run `rag.ipynb` from top to bottom.

Status: retrieval works. Connecting an LLM for answer generation is next.
