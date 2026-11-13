# 🔎 GenAI RAG Projects

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![LangChain](https://img.shields.io/badge/LangChain-RAG-1C3C3C)
![Groq](https://img.shields.io/badge/LLM-Groq-orange)
![Embeddings](https://img.shields.io/badge/Embeddings-Local%20(MiniLM)-purple)
![Colab](https://img.shields.io/badge/Runs%20on-Google%20Colab-F9AB00)

Four hands-on **Retrieval-Augmented Generation (RAG)** projects built with LangChain and **100% free tooling**: Groq for the LLM and local Sentence-Transformers embeddings, with Chroma or FAISS as the vector store.

Each notebook is a complete pipeline: load data → chunk → embed → store → retrieve → answer with sources.

## 📓 Projects

| # | Notebook | What it does | Vector store | UI | Open |
|---|---|---|---|---|---|
| 1 | `01_website_rag_chroma_streamlit` | Q&A over a website: loads pages, builds a knowledge base and shows which pages each answer came from | Chroma | Streamlit | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ashiqmuneeb/genai-rag-projects/blob/main/notebooks/01_website_rag_chroma_streamlit.ipynb) |
| 2 | `02_custom_website_chatbot_faiss_gradio` | Reusable chatbot for any website, with an optional `sitemap.xml` helper to collect URLs and a test that out-of-scope questions are refused | FAISS | Gradio | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ashiqmuneeb/genai-rag-projects/blob/main/notebooks/02_custom_website_chatbot_faiss_gradio.ipynb) |
| 3 | `03_pdf_qa_app_streamlit` | Ask questions about any PDF, with page-level sources and a "don't know" check | Chroma | Streamlit | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ashiqmuneeb/genai-rag-projects/blob/main/notebooks/03_pdf_qa_app_streamlit.ipynb) |
| 4 | `04_interview_questions_generator` | Turns a PDF into a Question + Answer CSV: an LLM generates questions, then a RAG step answers each one | FAISS | Gradio | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ashiqmuneeb/genai-rag-projects/blob/main/notebooks/04_interview_questions_generator.ipynb) |

## 🔄 Common Pipeline

```
Data source (website / PDF)
        │
        ▼
     Load  →  Chunk  →  Embed (all-MiniLM-L6-v2, local)  →  Vector store
                                                                │
        Question  ────────────────►  Retriever  ◄───────────────┘
                                        │
                                        ▼
                              Prompt + Groq LLM
                                        │
                                        ▼
                         Answer + source pages / URLs
```

## ✨ Highlights
- 💸 **Free to run:** Groq free tier for the LLM, local embeddings, no paid OpenAI key needed.
- 🔗 **Grounded answers:** sources (pages or URLs) are shown with each answer.
- 🛡️ **Hallucination checks:** prompts include a "say you don't know" rule, and the notebooks include in-domain and out-of-domain tests to prove it.
- 🧩 **Chunking strategy for question generation:** large chunks (about 3000 tokens) to generate questions, small chunks (about 500 tokens) to retrieve answers.
- 🖥️ **Three ways to interact:** notebook cells, Streamlit app, or Gradio chat UI.

## 🛠️ Tech Stack
| Area | Tools |
|---|---|
| Orchestration | LangChain |
| LLMs | Groq-hosted models (Llama 3.3 70B, GPT-OSS 20B / 120B, Qwen3 32B) |
| Embeddings | `sentence-transformers/all-MiniLM-L6-v2` (local) |
| Vector stores | Chroma, FAISS |
| Loaders | UnstructuredURLLoader, WebBaseLoader, PyPDFLoader |
| UI | Streamlit, Gradio |

## 🚀 How to Run (Google Colab)

1. Click an **Open in Colab** badge above.
2. Get a free API key at [console.groq.com](https://console.groq.com).
3. In Colab, open the **🔑 Secrets** panel (left sidebar), add a secret named `GROQ_API_KEY` and enable notebook access.
4. Run the cells top to bottom.

> The notebooks read the key with `google.colab.userdata`, so no API key is stored in the code. To run locally, replace that line with `os.environ["GROQ_API_KEY"]` and install `requirements.txt`.

## 📁 Structure
```
genai-rag-projects/
├── notebooks/
│   ├── 01_website_rag_chroma_streamlit.ipynb
│   ├── 02_custom_website_chatbot_faiss_gradio.ipynb
│   ├── 03_pdf_qa_app_streamlit.ipynb
│   └── 04_interview_questions_generator.ipynb
├── requirements.txt
├── LICENSE
└── README.md
```

## 🔮 Next Steps
- Combine these into one deployable FastAPI service
- Add re-ranking and evaluation (Recall@K, groundedness)
- Support multiple documents and conversation memory

## 📄 License
MIT License. See [LICENSE](LICENSE).
