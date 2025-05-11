# Psychic RAG Design of Experiments

## RAG Chunk Size DOE

A Jupyter notebook–based experiment to test how chunk size affects retrieval quality in a Retrieval‑Augmented Generation (RAG) pipeline using OpenAI embeddings and manual relevance scoring.

## 🚀 High‑Level Objectives

1. **Build a functional RAG pipeline** in a Jupyter notebook
2. **Run a single‑factor DOE** (Design of Experiments) on chunk size
3. **Generate and visualize results** that are simple, useful, and repeatable by the end of the day

---

## 🛠️ Prerequisites

* **Python 3.8+**
* **Jupyter Notebook** or **JupyterLab**
* **Git** (to clone the OpenAI Cookbook repo)
* **OpenAI API key** (set via a `.env` file)

---

## 📦 Installation

1. Clone this repo (or your working directory):

   ```bash
   git clone <your-repo-url>
   cd <your-repo-folder>
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Create a `.env` file in the project root:

   ```text
   OPENAI_API_KEY=sk-your_real_key_here
   ```

4. Install Jupyter widgets (optional, for progress bars):

   ```bash
   pip install ipywidgets
   jupyter nbextension enable --py widgetsnbextension
   ```

---

## ⚙️ Project Structure

```
rag-chunk-doe/
├── .env                # Your API key
├── requirements.txt    # Python dependencies
├── rag_chunk_doe.ipynb # Main experiment notebook
├── rag_chunk_doe_results.csv  # Output CSV (after running)
└── README.md           # This file
```

---

## 📝 Usage Tutorial

1. **Open the notebook**:

   ```bash
   jupyter notebook rag_chunk_doe.ipynb
   ```

2. **Load environment and configure client**:

   ```python
   from dotenv import load_dotenv
   import os
   from openai import OpenAI

   load_dotenv()
   client = OpenAI(api_key=os.getenv("OPENAI_API_KEY"))
   ```

3. **Part 1: Data Ingestion**

   * Clone or download the OpenAI Cookbook repository
   * Filter and load all `.md` files into memory

4. **Part 2: Chunking & Embedding**

   * Define `chunk_text(text, chunk_size)` using `GPT2TokenizerFast`
   * Loop over chunk sizes (e.g., 100, 250, 500, 1000 tokens)
   * Call `client.embeddings.create(...)` to embed each chunk
   * **Progress feedback**: prints and `tqdm` bars indicate activity

5. **Part 3: Retrieval Logic**

   * Define `retrieve_top_k(query, embeds, k=1)` using cosine similarity
   * Run your test questions against each chunk-size embedding set

6. **Part 4: Manual Scoring**

   * Display each retrieved chunk and prompt for a relevance score (1–5)
   * Log results to a Pandas DataFrame and export to CSV

7. **Part 5: Analysis & Plotting**

   * Compute the average score per chunk size
   * Plot a bar chart (chunk size vs. avg score)
   * Write your observations in the notebook’s markdown cells

---

## 📊 Interpreting Results

* **CSV output**: `rag_chunk_doe_results.csv` contains columns:

  * `chunk_size`, `question`, `score`
* **Visualization**: a bar chart shows which chunk size performed best
* **Observations**: jot down why a certain size wins (e.g., context vs. noise)

---

## ⚙️ Customization & Extensions

* **Chunk sizes**: tweak `sizes = [100, 250, 500, 1000]` to other values
* **Questions**: add or swap your own test queries in the questions list
* **Auto‑scoring**: integrate a GPT‑4 prompt to auto‑rate relevance
* **Parametrization**: use Papermill to rerun the notebook with different settings

---

## 📝 License

This experiment is released under the [MIT License](LICENSE).

Happy chunking! — *Skippy*
