# thesis-rag

My first RAG project. You ask a question about a research paper, and it answers using only the paper's own text and tells you which pages it used.

## How it works

1. The PDF is split into small chunks of text.
2. Each chunk is turned into numbers (an embedding) with BAAI/bge-small-en-v1.5.
3. Your question is turned into numbers the same way, and FAISS finds the chunks that are closest to it.
4. Those chunks and your question are sent to a local LLM through Ollama, which writes the answer.

## Step by step setup

**Step 1: Get the project**

```bash
git clone <your-repo-link>
cd thesis-rag
```

**Step 2: Make a virtual environment and install the libraries**

```bash
python -m venv .venv
source .venv/bin/activate
pip install pymupdf python-docx sentence-transformers faiss-cpu ollama
```

**Step 3: Add your paper**

Create a folder named `papers` next to the notebook and put your PDF inside it.

**Step 4: Install Ollama and download a model**

Install Ollama from https://ollama.com, then run:

```bash
ollama pull llama3.2:3b
```

Check that it is running with `ollama list`. You should see the model in the list.

**Step 5: Set the model name**

In the notebook, find the cell with `ask` and make sure `LLM` matches the model you pulled:

```python
LLM = "llama3.2:3b"
```

**Step 6: Run the notebook**

Open `rag.ipynb` and run the cells from top to bottom. The embedding cell takes a bit the first time.

**Step 7: Ask a question**

In a new cell at the end, run:

```python
ask("What is the main contribution of this paper?")
```

The answer appears under the cell, followed by the sources (file and page).

## Common problems

No output for a long time: the first answer is slow because the model has to load into memory, and a CPU is slower than a GPU. A smaller model is faster.

`NameError: name 'ask' is not defined`: run all the cells above it first, in order.

Cannot connect to Ollama: make sure Ollama is running. If you use WSL and Ollama is installed on Windows, WSL may not reach it, so install Ollama inside WSL instead.

## Status

Retrieval and answer generation both work.