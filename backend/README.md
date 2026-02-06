---
title: AI Research Paper Helper API
emoji: 📚
colorFrom: indigo
colorTo: purple
sdk: docker
app_port: 7860
pinned: false
license: mit
---

# AI Research Paper Helper API

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.109-009688.svg)](https://fastapi.tiangolo.com)

An ML-powered FastAPI backend for research paper analysis, summarization, equation explanation, and RAG-based Q&A. Designed to work with browser extensions for seamless research assistance.

## ✨ Features

- **📝 Multi-Level Summarization** - Generate brief, standard, and detailed summaries
- **🔢 Equation Explanation** - Parse and explain LaTeX mathematical equations
- **🎯 Key Point Extraction** - Identify main contributions and concepts
- **💬 RAG-based Q&A** - Index papers and ask natural language questions

## 🚀 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | API information |
| `/health` | GET | Health check & model status |
| `/docs` | GET | Interactive Swagger documentation |
| `/summarize` | POST | Generate multi-level summaries |
| `/explain-equations` | POST | Explain LaTeX equations |
| `/extract-key-points` | POST | Extract key contributions |
| `/rag/index` | POST | Index a paper for RAG queries |
| `/rag/query` | POST | Query indexed paper |

## 🔧 Configuration

The API supports multiple inference modes:

| Mode | Description |
|------|-------------|
| `api` | Uses external LLM APIs (Groq/OpenRouter) - **Recommended for HF Spaces** |
| `local` | Uses local HuggingFace models (requires GPU for best performance) |

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `AIHELPER_API_MODE` | Inference mode (`local` or `api`) | `api` |
| `AIHELPER_GROQ_API_KEY` | Groq API key for fast inference | - |
| `AIHELPER_OPENROUTER_API_KEY` | OpenRouter API key (fallback) | - |

## 🏃 Running Locally

### Quick Start

```bash
# Clone and navigate to backend
cd backend

# Create virtual environment
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env
# Edit .env with your API keys

# Run the server
python main.py
```

The API will be available at `http://localhost:8000`

### With Docker

```bash
docker build -t ai-research-helper .
docker run -p 7860:7860 -e AIHELPER_GROQ_API_KEY=your_key ai-research-helper
```

## 📖 API Usage Examples

### Summarize Text

```bash
curl -X POST "http://localhost:8000/summarize" \
  -H "Content-Type: application/json" \
  -d '{"content": "Your research paper text here..."}'
```

### Explain Equation

```bash
curl -X POST "http://localhost:8000/explain-equations" \
  -H "Content-Type: application/json" \
  -d '{"equation": "E = mc^2"}'
```

### RAG Query

```bash
# First, index a paper
curl -X POST "http://localhost:8000/rag/index" \
  -H "Content-Type: application/json" \
  -d '{"paper_id": "paper123", "text": "Full paper content..."}'

# Then query it
curl -X POST "http://localhost:8000/rag/query" \
  -H "Content-Type: application/json" \
  -d '{"paper_id": "paper123", "question": "What is the main contribution?"}'
```

## 🧪 Running Tests

```bash
# Install test dependencies (included in requirements.txt)
pip install pytest pytest-asyncio

# Run all tests
pytest tests/ -v

# Run specific test file
pytest tests/test_summarizer.py -v
```

## 🛠️ Tech Stack

- **FastAPI** - High-performance async web framework
- **Sentence Transformers** - Lightweight embeddings (all-MiniLM-L6-v2)
- **FAISS** - Efficient vector similarity search
- **Groq/OpenRouter** - Fast LLM inference via API
- **SpaCy** - NLP processing and text analysis
- **SymPy** - Mathematical equation parsing

## 📁 Project Structure

```
backend/
├── main.py              # FastAPI app entry point
├── config.py            # Configuration management
├── Dockerfile           # Container configuration
├── requirements.txt     # Python dependencies
├── routers/             # API endpoint handlers
│   ├── summarize.py
│   ├── equations.py
│   ├── keypoints.py
│   └── rag.py
├── services/            # Business logic
│   ├── summarizer.py
│   ├── equation_explainer.py
│   ├── keyword_extractor.py
│   └── rag_engine.py
├── ml/                  # ML pipeline
│   ├── models.py
│   ├── embeddings.py
│   └── text_processor.py
└── tests/               # Test suite
```

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## 📄 License

MIT License - See [LICENSE](LICENSE) for details.
